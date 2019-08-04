## usersテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false　add_index|
|password|string|null: false add_index|
|address|string|null: false add_index|

### Association
- has_many :messages
- has_many :members
- has_many :groups, through: :members

## messagesテーブル

|Column|Type|Options|
|------|----|-------|
|body|text|null: false|
|img|string||
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :users
- belongs_to :groups

### validation
- validates :body_or_img, presence: true
`private`
  `def body_or_img`
    `body.presence or img.presence`
  `end`
`end`
`テキストもしくは画像が挿入されていれば許可`

## groupsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null :false add_index|

### Association
- has_many :messages
- has_many :members
- has_many :users, through: :members

## membersテーブル

|Column|Type|Options|
|------|----|-------|
|user_id|integer|null: false, foreign_key: true|
|group_id|integer|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user