---
name: NEST_ARCHITECTURE
description: NestJS를 최초 구성할때 주로 사용하는 아키텍처 모음입니다. NestJS 프로젝트를 생성할때 참고하면 좋습니다.
triger: model_decision
---

# NestJS Architecture

NestJS는 여러 서비스를 구현할 수 있게 도와줍니다. 프로젝트마다 관리하기 용이한 방식의 아키텍처들을 모아두었습니다.

## Architecture List

### Standard Modular

가장 보편적이며 NestJS의 기본 철학에 충실한 구조입니다. 소규모~중규모 프로젝트에서 매우 효율적입니다.

#### Standard Modular 개념

> 기능(도메인)별로 폴더를 나누고, 각 폴더 내부에 계층을 둡니다.

#### Standard Modular 구조

```plaintext
src/
├── common/                 # 공통 필터, 인터셉터, 데코레이터, 유틸리티
├── config/                 # 환경 변수 및 설정 관련
├── modules/
│   ├── user/
│   │   ├── dto/            # Data Transfer Objects (Named Export 권장)
│   │   ├── entities/       # Database Entities
│   │   ├── user.controller.ts
│   │   ├── user.service.ts
│   │   ├── user.repository.ts # TypeORM/Prisma 의존성 분리용
│   │   ├── user.module.ts
│   │   └── index.ts        # 외부 모듈용 배럴 파일
│   └── auth/
├── main.ts
└── app.module.ts
```

#### Standard Modular Tip

- Service에서 모든 것을 하지 마세요. DB 접근 로직은 Repository로 분리하여 서비스는 비즈니스 로직에만 집중하게 합니다.
- 사용자 룰에 언급된 것처럼 **Barrel 파일**(index.ts)은 외부 모듈에서 참조할 때만 사용하고, 모듈 내부에서는 직접 참조하여 순환 참조를 방지합니다.

### Hexagonal Lite

비즈니스 로직이 복잡하거나, 인프라(DB, 외부 API)가 바뀔 가능성이 있는 대규모 프로젝트에서 선호합니다.

#### Hexagonal Lite 개념

코드의 의존성을 **의존성 주입**(DI)을 통해 역전시켜, 외부 기술(DB, Library)로부터 순수한 비즈니스 로직을 보호합니다.

#### Hexagonal Lite 구조

```plaintext
src/
├── domain/                 # 순수 비즈니스 로직 & 인터페이스 (추상화 계층)
│   ├── user/
│   │   ├── user.model.ts
│   │   └── user.repository.interface.ts
├── application/            # 유스케이스 (도메인 서비스를 활용한 흐름 제어)
│   └── user/
│       └── user.service.ts
├── infrastructure/         # 외부 구현체 (DB, Mail, Redis 등)
│   └── persistence/
│       └── typeorm/
│           └── user.typeorm.repository.ts
└── interface/              # API 진입점
    └── http/
        ├── user.controller.ts
        └── dto/
```

#### Hexagonal Lite Tip

- interface 계층(Controller)은 application 계층에만 의존해야 합니다.
- 함수형 프로그래밍 스타일을 선호하신다면, 도메인 로직을 클래스가 아닌 **순수 함수**(Pure Function)들의 집합으로 작성하고 Service에서 이를 조합(Composition)하는 방식을 추천합니다.

### CQRS

읽기 작업과 쓰기 작업의 로직이 완전히 다를 때(예: 통계 쿼리는 복잡하고, 생성은 단순함) 사용합니다.

#### CQRS 개념

상태를 변경하는 Command와 데이터를 조회하는 Query를 분리하여 확장성을 높입니다.

#### CQRS 도구

@nestjs/cqrs 라이브러리 활용.

#### CQRS 구조

```plaintext
src/modules/user/
├── commands/               # Create, Update, Delete 관련 핸들러
│   ├── create-user.command.ts
│   └── create-user.handler.ts
├── queries/                # Find, Get, Search 관련 핸들러
│   ├── get-user.query.ts
│   └── get-user.handler.ts
├── events/                 # 사이드 이펙트 처리를 위한 이벤트 핸들러
└── user.module.ts
```

#### CQRS Tip

- 모든 곳에 CQRS를 적용하지 마세요. 오버헤드가 큽니다. 도메인이 너무 비대해져서 메서드가 20~30개가 넘어갈 때 분리하는 것이 적절합니다.

## Code Conventions

1. **Named Export 우선**: default export는 지양합니다. 리팩토링 시 IDE의 도움을 받기 어렵고 트리쉐이킹 효율이 떨어집니다.
2. **DTO & Validation**: 모든 입구에는 class-validator와 class-transformer를 사용하여 엄격한 화이트리스트 검증을 수행합니다.
3. **Custom Exception Filter**: 서비스 전체에서 일관된 에러 응답 구조를 갖도록 공통 필터를 구축합니다.
4. **Immutability**: 입력받은 객체를 직접 수정하지 않고, 새로운 객체를 반환하는 패턴을 유지합니다. (사용자님의 FP 지향 규칙 준수)
5. **Interface-driven DI**: Service가 특정 클래스에 의존하지 않고 인터페이스(또는 Abstract Class)에 의존하게 하여 테스트 시 Mocking을 용이하게 합니다.

```typescript
// 예시
@Injectable()
export class UserService {
  constructor(
    @Inject(IUserRepository) private readonly userRepository: IUserRepository,
  ) {}
}
```
