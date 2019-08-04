## usersテーブル

|Column|Type|Options|
|------|----|-------|
|name|string|null: false index: true|

### Association
- has_many :messages
- has_many :members
- has_many :groups, through: :members

## messagesテーブル

|Column|Type|Options|
|------|----|-------|
|body|text||
|img|string||
|user|references|null: false, foreign_key: true|
|group|references|null: false, foreign_key: true|

### Association
- belongs_to :user
- belongs_to :group

### validation
- validates :body_or_img, presence: true

```
private
  def body_or_img
    body.presence or img.presence
  end`
end
```

`テキストもしくは画像が挿入されていれば許可`

## groupsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null :false|

### Association
- has_many :messages
- has_many :members
- has_many :users, through: :members

## membersテーブル

|Column|Type|Options|
|------|----|-------|
|user|references|null: false, foreign_key: true|
|group|references|null: false, foreign_key: true|

### Association
- belongs_to :group
- belongs_to :user