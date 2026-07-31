# 26. Kiến trúc dự án RPG Unity

[⬅ Quay lại](25-youtube-nen-xem.md)

## Mục lục

1. [Tổng quan](#tong-quan)
2. [Nguyên tắc thiết kế](#nguyen-tac-thiet-ke)
3. [Cấu trúc Scene](#cau-truc-scene)
4. [Cấu trúc Prefab](#cau-truc-prefab)
5. [Cấu trúc thư mục](#cau-truc-thu-muc)
6. [Kiến trúc nhân vật](#kien-truc-nhan-vat)
7. [Prefab và ScriptableObject](#prefab-va-scriptableobject)
8. [Kết luận](#ket-luan)

> Gợi ý: nếu bạn mới bắt đầu, hãy đọc [25. Youtube nên xem](25-youtube-nen-xem.md) trước để làm quen với nguồn học và phong cách làm việc, rồi quay lại module này.

---

<a id="tong-quan"></a>

## 1. Tổng quan

Đây là một kiến trúc phù hợp cho dự án RPG Unity và có thể mở rộng lâu dài. Mục tiêu của mô hình này là:

- Prefab chịu trách nhiệm cấu trúc và hành vi.
- ScriptableObject chịu trách nhiệm dữ liệu.
- Player, Enemy và NPC dùng chung các component cốt lõi như CharacterMovement, SkillCaster, CharacterHealth...
- Dễ mở rộng khi số lượng nhân vật và hệ thống tăng lên.

Kiến trúc này đi theo hướng component-based và data-driven.

---

<a id="nguyen-tac-thiet-ke"></a>

## 2. Nguyên tắc thiết kế

### 2.1 Tách dữ liệu khỏi logic

- Dữ liệu nên nằm ở ScriptableObject.
- Logic nên nằm ở component hoặc controller.

### 2.2 Dùng component chung cho nhiều nhân vật

- Player, Enemy, NPC có thể dùng chung movement, health, skill.
- Chỉ khác nhau ở controller và dữ liệu cấu hình.

### 2.3 Giữ prefab sạch và rõ mục đích

- Prefab nên chứa cấu trúc, visual và collider cần thiết.
- Không nên đặt quá nhiều logic trực tiếp vào prefab.

### 2.4 Tổ chức project rõ ràng

- Thư mục nên có tên dễ hiểu và dễ tìm.
- Khi dự án lớn, việc phân tầng đúng sẽ giúp team làm việc hiệu quả hơn.

---

<a id="cau-truc-scene"></a>

## 3. Cấu trúc Scene

```text
Boot Scene
│
├── Bootstrap
│
├── Systems
│   ├── InputSystem
│   ├── CameraSystem
│   ├── AudioSystem
│   ├── PoolSystem
│   ├── SaveSystem
│   ├── QuestSystem
│   ├── InventorySystem
│   ├── CombatSystem
│   ├── UISystem
│   └── LocalizationSystem
│
├── Environment
│   ├── Terrain
│   ├── Buildings
│   ├── Trees
│   ├── Props
│   └── Water
│
├── SpawnPoints
│   ├── PlayerSpawn
│   ├── NPCSpawn
│   └── EnemySpawn
│
├── NPCs
├── Monsters
├── DynamicObjects
├── Lighting
├── Canvas
└── EventSystem
```

### Lưu ý quan trọng

- Player được spawn runtime.
- Không đặt Player cố định trong Scene.
- Không đặt GameManager trong Player.

---

<a id="cau-truc-prefab"></a>

## 4. Cấu trúc Prefab

```text
Player
│
├── [Components]
│   ├── Transform
│   ├── Character
│   ├── PlayerController
│   ├── PlayerInput
│   ├── CharacterMovement
│   ├── CharacterMotor
│   ├── CharacterHealth
│   ├── CharacterMana
│   ├── CharacterStats
│   ├── SkillCaster
│   ├── Inventory
│   ├── Equipment
│   ├── CharacterStateMachine
│   ├── AnimatorBridge
│   ├── AudioBridge
│   └── TargetProvider
│
├── Visual
│   ├── SpriteRig
│   ├── Body
│   ├── Head
│   ├── Hair
│   ├── Weapon
│   ├── Cape
│   └── Shadow
│
├── Sockets
│   ├── CameraTarget
│   ├── AttackPoint
│   ├── LeftHand
│   ├── RightHand
│   ├── HeadSocket
│   ├── Feet
│   └── InteractionPoint
│
├── Sensors
│   ├── GroundCheck
│   ├── WallCheck
│   └── LedgeCheck
│
├── Combat
│   ├── Hitboxes
│   └── Hurtboxes
│
├── Audio
└── VFX
```

Cấu trúc này giúp prefab rõ mục đích, dễ debug và dễ mở rộng khi thêm tính năng mới.

---

<a id="cau-truc-thu-muc"></a>

## 5. Cấu trúc thư mục

### 5.1 Script folder

```text
Assets/
└── Scripts/
    ├── Core/
    │   ├── Character/
    │   ├── Combat/
    │   ├── Inventory/
    │   ├── Interaction/
    │   └── Sensors/
    ├── Player/
    ├── AI/
    ├── Camera/
    ├── UI/
    ├── Audio/
    ├── Save/
    ├── Quest/
    ├── Systems/
    └── Utilities/
```

### 5.2 Asset folder

```text
Assets/
└── _Project/
    ├── Art/
    ├── Animations/
    ├── Materials/
    ├── Models/
    ├── Prefabs/
    ├── ScriptableObjects/
    ├── Scenes/
    ├── Audio/
    ├── Shaders/
    ├── Addressables/
    ├── Settings/
    ├── ThirdParty/
    └── Plugins/
```

### Gợi ý phân chia

- Core: các hệ thống dùng chung cho nhiều nhân vật.
- Player: logic riêng của người chơi.
- AI: hệ thống NPC và enemy điều khiển bằng AI.
- Systems: các hệ thống toàn cục như save, quest, inventory.

---

<a id="kien-truc-nhan-vat"></a>

## 6. Kiến trúc nhân vật

```text
Keyboard / Gamepad
        │
        ▼
PlayerInput
        │
        ▼
PlayerController
        │
        ├────────────► CharacterMovement
        │
        ├────────────► SkillCaster
        │
        ├────────────► InteractionController
        │
        └────────────► Inventory
                              │
                              ▼
                     CharacterStateMachine
                              │
                              ▼
                     AnimatorBridge
                              │
            ┌─────────────────┼─────────────────┐
            ▼                 ▼                 ▼
        Animator             VFX              Audio
```

AI cũng có thể dùng chung pipeline:

```text
VisionSensor
      │
      ▼
AIBrain
      │
      ▼
AIController
      │
      ├────────► CharacterMovement
      ├────────► SkillCaster
      └────────► InteractionController
```

### Ý nghĩa

- Input và controller quyết định hành vi.
- Movement, combat, interaction là các module riêng.
- Animator, VFX, Audio là tầng phản hồi cho hành vi.

---

<a id="prefab-va-scriptableobject"></a>

## 7. Prefab và ScriptableObject

```text
PF_Character_Base
        │
        ├──────── PF_Player
        │
        ├──────── PF_Goblin
        │               │
        │               ├──── PF_Goblin_Elite
        │               ├──── PF_Goblin_Mage
        │               └──── PF_Goblin_Boss
        │
        ├──────── PF_Wolf
        │
        ├──────── PF_Merchant
        │
        └──────── PF_Boss
```

### Mối quan hệ giữa Prefab và ScriptableObject

```text
PF_Goblin
        │
        └──────── CharacterData
                     │
                     └──── SO_Goblin.asset
```

### Quy tắc nên nhớ

- Prefab chỉ chứa cấu trúc và behavior.
- ScriptableObject chứa dữ liệu như:
  - HP
  - Mana
  - Damage
  - Speed
  - Skills
  - Loot
  - XP
  - Resistances
  - AI Config

---

<a id="ket-luan"></a>

## 8. Kết luận

Kiến trúc này giúp bạn xây dựng dự án RPG Unity theo hướng rõ ràng, dễ bảo trì và có thể phát triển lâu dài. Nếu bạn tuân thủ các nguyên tắc trên từ đầu, việc thêm feature mới, thêm enemy mới hoặc mở rộng hệ thống sẽ trở nên dễ dàng hơn rất nhiều.
