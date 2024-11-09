# Chatwork API v2<br>Google Apps Script ライブラリ

Google Apps Script スクリプト ID: `1_G2DWvA4_JU87Tc40cABnA3G8nxR2e_t1HJ7Wy_qS557GAfW7RolBp7E`

https://github.com/whalderman/Apps-Script-Chatwork-API/assets/8446860/fff0ac8a-8328-4d8d-bb4e-64830cec4b73

## ドキュメント

このライブラリは、Google Apps Script から Chatwork API を利用するための関数を提供します。

### 関数

#### `getMe(token)`

自分自身の情報を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-me)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。

##### 戻り値

- [`Me`](#Me): 自分自身の情報を含むオブジェクト。

---

#### `getMyStatus(token)`

自分の未読数、未読 To 数、未完了タスク数を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-my-status)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。

##### 戻り値

- [`MyStatus`](#MyStatus): 未読数、未読 To 数、未完了タスク数を含むオブジェクト。

---

#### `getMyTasks(token, queryParams)`

自分のタスク一覧を最大 100 件まで取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-my-tasks)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- `queryParams` {object}: 取得条件を指定するパラメータ。

  - `assigned_by_account_id` {string | number}: タスクを割り当てたユーザーのアカウント ID。
  - `status` {'open' | 'done'}: タスクのステータス。 `open` は未完了、`done` は完了。

  #### 戻り値

- [`MyTask[]`](#MyTask): 自分のタスク情報を含むオブジェクトの配列。

---

#### `getContacts(token)`

自分のコンタクト一覧を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-contacts)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。

##### 戻り値

- [`Contact[]`](#Contact): コンタクト情報を含むオブジェクトの配列。

---

#### `getRooms(token)`

チャット一覧を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。

##### 戻り値

- [`RoomInfo[]`](#RoomInfo): チャットルーム情報を含むオブジェクトの配列。

---

#### `postRooms(token, formData)`

新しいグループチャットを作成します。

- HTTP メソッド: POST (新規作成)
- [参照リンク](https://developer.chatwork.com/reference/post-rooms)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `formData` {object}: ルーム作成に必要な情報。
  - **必須** `name` {string}: グループチャットの名前。
  - `description` {string}: グループチャットの概要。
  - `link` {number}: 招待リンクを作成するか (0: 作成しない, 1: 作成する)。
  - `link_code` {string}: 招待リンクのパス部分。省略するとランダムな文字列が生成されます。
  - `link_need_acceptance` {number}: 参加に管理者の承認を必要とするか (0: 不要, 1: 必要)。
  - **必須** `members_admin_ids` {string | (string | number)[]}: 管理者権限のユーザーのアカウント ID（カンマ区切りまたは配列）。
  - `members_member_ids` {string | (string | number)[]}: メンバー権限のユーザーのアカウント ID（カンマ区切りまたは配列）。
  - `members_readonly_ids` {string | (string | number)[]}: 閲覧のみ権限のユーザーのアカウント ID（カンマ区切りまたは配列）。
  - `icon_preset` {string}: グループチャットのアイコンの種類。  
    指定可能な値は `group`, `check`, `document`, `meeting`, `event`, `project`, `business`, `study`, `security`, `star`, `idea`, `heart`, `magcup`, `beer`, `music`, `sports`, `travel`。

##### 戻り値

- [`RoomsPostResponse`](#RoomsPostResponse): 作成したチャットルームの情報を含むオブジェクト。

---

#### `getRoom(token, roomId)`

チャットの情報（名前、アイコン、種類など）を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。

##### 戻り値

- [`RoomInfoWithDescription`](#RoomInfoWithDescription): チャットルームの情報を含むオブジェクト。

---

#### `putRoom(token, roomId, formData)`

チャットの情報（名前、アイコンなど）を変更します。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `formData` {object}: 変更するチャットの情報。
  - `name` {string}: チャットの名前。
  - `description` {string}: チャットの概要。
  - `icon_preset` {string}: チャットのアイコンの種類。指定可能な値は `group`, `check`, `document`, `meeting`, `event`, `project`, `business`, `study`, `security`, `star`, `idea`, `heart`, `magcup`, `beer`, `music`, `sports`, `travel`。

##### 戻り値

- [`RoomPutResponse`](#RoomPutResponse): 更新されたチャットルームの情報を含むオブジェクト。

---

#### `deleteRooms(token, roomId, formData)`

グループチャットを退席、または削除します。

**注意:** グループチャットを削除すると、メッセージ、タスク、ファイルがすべて削除されます。(一度削除すると元に戻せません。)

- HTTP メソッド: DELETE (削除) (削除)
- [参照リンク](https://developer.chatwork.com/reference/delete-rooms-room_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `formData` {object}: 操作の種類を指定するオブジェクト。
  - **必須** `action_type` {'leave' | 'delete'}: 操作の種類。 `leave` は退席、 `delete` は削除。

#### `getRoomMembers(token, roomId)`

チャットのメンバー一覧を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-members)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。

##### 戻り値

- [`RoomMember[]`](#RoomMember): メンバー情報を含むオブジェクトの配列。

---

#### `putRoomMembers(token, roomId, formData)`

チャットのメンバーを一括で変更します。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id-members)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `formData` {object}: メンバー情報を含むオブジェクト。
  - **必須** `members_admin_ids` {string | (string | number)[]}: 管理者権限のユーザーのアカウント ID（カンマ区切りまたは配列）。 少なくとも 1 人以上必要。
  - `members_member_ids` {string | (string | number)[]}: メンバー権限のユーザーのアカウント ID（カンマ区切りまたは配列）。
  - `members_readonly_ids` {string | (string | number)[]}: 閲覧のみ権限のユーザーのアカウント ID（カンマ区切りまたは配列）。

##### 戻り値

- [`RoomMembersPutResponse`](#RoomMembersPutResponse): 更新されたメンバー情報を含むオブジェクト。

---

#### `getRoomMessages(token, roomId, queryParams)`

チャットのメッセージ一覧を最大 100 件まで取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-messages)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `queryParams` {object}: メッセージ取得条件を指定するパラメータ。
  - `force` {boolean}: 強制的に最大件数まで取得するかどうか。 `false` (デフォルト) の場合は前回取得分からの差分のみ、 `true` の場合は強制的に最新のメッセージを最大 100 件取得。

##### 戻り値

- [`Message[]`](#Message): メッセージ情報を含むオブジェクトの配列。

---

#### `postRoomMessage(token, roomId, formData)`

チャットに新しいメッセージを投稿します。

- HTTP メソッド: POST (新規作成)
- [参照リンク](https://developer.chatwork.com/reference/post-rooms-room_id-messages)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `formData` {object}: メッセージ情報を含むオブジェクト。
  - **必須** `body` {string}: メッセージ本文。
  - `self_unread` {boolean}: 投稿メッセージを自分から見て未読にするか。 `false` (デフォルト) は既読、 `true` は未読。

##### 戻り値

- [`UpdatedMessage`](#UpdatedMessage): 投稿したメッセージの情報を含むオブジェクト。

---

#### `putRoomMessagesRead(token, roomId, formData)`

チャットのメッセージを既読にします。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id-messages-read)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `formData` {object}: 既読にするメッセージの情報。
  - **必須** `message_id` {string}: 既読にするメッセージの ID。 指定した ID までのメッセージが既読になります。

##### 戻り値

- [`RoomMessagesReadPutResponse`](#RoomMessagesReadPutResponse): 未読数とメンション数を含むオブジェクト。

---

#### `putRoomMessagesUnread(token, roomId, formData)`

チャットのメッセージを未読にします。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id-messages-unread)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `formData` {object}: 未読にするメッセージの情報。
  - **必須** `message_id` {string}: 未読にするメッセージの ID。 指定した ID 以降のメッセージが未読になります。

##### 戻り値

- [`RoomMessagesUnreadPutResponse`](#RoomMessagesUnreadPutResponse): 未読数とメンション数を含むオブジェクト。

---

#### `getRoomMessage(token, roomId, messageId)`

チャットのメッセージを取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-messages-message_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `messageId` {number}: メッセージ ID。

##### 戻り値

- [`Message`](#Message): メッセージの情報を含むオブジェクト。

---

#### `putRoomMessage(token, roomId, messageId, formData)`

チャットのメッセージを変更します。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id-messages-message_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `messageId` {number}: メッセージ ID。
- **必須** `formData` {object}: 変更するメッセージの情報。
  - **必須** `body` {string}: 更新するメッセージ本文。

##### 戻り値

- [`UpdatedMessage`](#UpdatedMessage): 更新されたメッセージの情報を含むオブジェクト。

---

#### `deleteRoomMessage(token, roomId, messageId)`

チャットのメッセージを削除します。

- HTTP メソッド: DELETE (削除)
- [参照リンク](https://developer.chatwork.com/reference/delete-rooms-room_id-messages-message_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `messageId` {number}: メッセージ ID。

##### 戻り値

- {object}: 空のオブジェクト。

---

#### `getRoomTasks(token, roomId, queryParams)`

チャットのタスク一覧を最大 100 件まで取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-tasks)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `queryParams` {object}: 取得条件を指定するパラメータ。
  - `account_id` {number}: 担当者のアカウント ID。
  - `assigned_by_account_id` {string | number}: タスクを割り当てたユーザーのアカウント ID。
  - `status` {'open' | 'done'}: タスクのステータス。 `open` は未完了、`done` は完了。

##### 戻り値

- [`Task[]`](#Task): タスク情報を含むオブジェクトの配列。

---

#### `postRoomTasks(token, roomId, formData)`

チャットに新しいタスクを追加します。

- HTTP メソッド: POST (新規作成)
- [参照リンク](https://developer.chatwork.com/reference/post-rooms-room_id-tasks)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `formData` {object}: タスク情報を含むオブジェクト。
  - **必須** `body` {string}: タスクの内容。
  - **必須** `to_ids` {string | (string | number)[]}: 担当者にしたいユーザーのアカウント ID（カンマ区切りまたは配列）。
  - `limit` {number | string}: タスクの期限。Unix 時間（秒）で指定。
  - `limit_type` {'none' | 'date' | 'time'}: タスクの期限の種類。 `none` は期限なし、 `date` は日付期限、 `time` は時間期限。 デフォルトは `time`。

##### 戻り値

- [`PostTasksResponse`](#PostTasksResponse): 追加されたタスクの情報を含むオブジェクト。

---

#### `getRoomTask(token, roomId, taskId)`

チャットのタスクの情報を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-tasks-task_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `taskId` {number}: タスク ID。

##### 戻り値

- [`Task`](#Task): タスクの情報を含むオブジェクト。

---

#### `putRoomTaskStatus(token, roomId, taskId, formData)`

チャットのタスクの完了状態を変更します。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id-tasks-task_id-status)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `taskId` {number}: タスク ID。
- **必須** `formData` {object}: タスクの完了状態を含むオブジェクト。
  - **必須** `body` {'open' | 'done'}: タスクの完了状態。 `done` は完了、 `open` は未完了。

##### 戻り値

- [`TaskIdResponse`](#TaskIdResponse): タスク ID を含むオブジェクト。

---

#### `getRoomFiles(token, roomId, queryParams)`

チャットのファイル一覧を最大 100 件まで取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-files)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `queryParams` {object}: 取得条件を指定するパラメータ。
  - `account_id` {number}: アップロードしたユーザーのアカウント ID。

##### 戻り値

- [`File[]`](#File): ファイル情報を含むオブジェクトの配列。

---

#### `postRoomFiles(token, roomId, formData)`

チャットに新しいファイルをアップロードします。

- HTTP メソッド: POST (新規作成)
- [参照リンク](https://developer.chatwork.com/reference/post-rooms-room_id-files)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `formData` {object}: ファイル情報を含むオブジェクト。
  - `file` {Blob | Uint8Array}: アップロードするファイルのバイナリ。(必須, 最大 5MB)
  - `message` {string}: ファイルに添付するメッセージ。

##### 戻り値

- [`UploadedFiles`](#UploadedFiles): アップロードされたファイルの情報を含むオブジェクト。

---

#### `getRoomFile(token, roomId, fileId, queryParams)`

チャットのファイルの情報を取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-files-file_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- **必須** `fileId` {number}: ファイル ID。
- `queryParams` {object}: 取得条件を指定するパラメータ。
  - `create_download_url` {boolean}: ダウンロード URL を作成するか。作成された URL は 30 秒間有効。

##### 戻り値

- [`DownloadableFile`](#DownloadableFile): ファイル情報とダウンロード URL を含むオブジェクト。

---

#### `getRoomLink(token, roomId)`

チャットへの招待リンクを取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-rooms-room_id-link)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。

##### 戻り値

- [`RoomInvitationLink`](#RoomInvitationLink): 招待リンク情報を含むオブジェクト。

---

#### `postRoomLink(token, roomId, formData)`

チャットへの招待リンクを作成します。
すでに招待リンクが作成されている場合は 400 エラーを返します。

- HTTP メソッド: POST (新規作成)
- [参照リンク](https://developer.chatwork.com/reference/post-rooms-room_id-link)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `formData` {object}: 招待リンク情報を含むオブジェクト。
  - `code` {string}: 招待リンクのパス部分。省略するとランダムな文字列が生成されます。
  - `need_acceptance` {boolean}: 参加に管理者の承認を必要とするか。
  - `description` {string}: 招待リンクのページに表示される説明文。

##### 戻り値

- [`RoomInvitationLink`](#RoomInvitationLink): 変更後の招待リンク情報を含むオブジェクト。

---

#### `putRoomLink(token, roomId, formData)`

チャットへの招待リンクを変更します。
招待リンクが無効になっている場合は 400 エラーを返します。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-rooms-room_id-link)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。
- `formData` {object}: 招待リンク情報を含むオブジェクト。
  - `code` {string}: 招待リンクのパス部分。省略するとランダムな文字列が生成されます。
  - `need_acceptance` {boolean}: 参加に管理者の承認を必要とするか。
  - `description` {string}: 招待リンクのページに表示される説明文。

##### 戻り値

- [`RoomInvitationLink`](#RoomInvitationLink): 変更後の招待リンク情報を含むオブジェクト。

---

#### `deleteRoomLink(token, roomId)`

チャットへの招待リンクを削除します。招待リンクが無効になっている場合は 400 エラーを返します。

- HTTP メソッド: DELETE (削除)
- [参照リンク](https://developer.chatwork.com/reference/delete-rooms-room_id-link)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `roomId` {number}: ルーム ID。

##### 戻り値

- [`RoomInvitationLink`](#RoomInvitationLink): 削除された招待リンク情報を含むオブジェクト。

---

#### `getIncomingRequests(token)`

自分へのコンタクト承認依頼一覧を最大 100 件まで取得します。

- HTTP メソッド: GET (参照)
- [参照リンク](https://developer.chatwork.com/reference/get-incoming_requests)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。

##### 戻り値

- [`ContactRequest[]`](#ContactRequest): コンタクト承認依頼情報を含むオブジェクトの配列。

---

#### `putIncomingRequests(token, requestId)`

自分へのコンタクト承認依頼を承認します。

- HTTP メソッド: PUT (更新)
- [参照リンク](https://developer.chatwork.com/reference/put-incoming_requests-request_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `requestId` {number}: リクエスト ID。

##### 戻り値

- [`ContactRequestApprovalResponse`](#ContactRequestApprovalResponse): 承認されたコンタクト情報（リクエスト ID を除く）を含むオブジェクト。

---

#### `deleteIncomingRequest(token, requestId)`

自分へのコンタクト承認依頼を拒否します。

- HTTP メソッド: DELETE (削除)
- [参照リンク](https://developer.chatwork.com/reference/delete-incoming_requests-request_id)

##### パラメータ

- **必須** `token` {string}: [Chatwork API トークン]。
- **必須** `requestId` {number}: リクエスト ID。

##### 戻り値

- {object}: 空のオブジェクト。

### Type Definitions

#### `Me`

提供された API トークンに関連付けられたユーザーに関する情報を含むオブジェクト。

```typescript
interface Me {
  // ユーザーのID
  account_id: number;
  // ユーザーのルームID
  room_id: number;
  // ユーザーの名
  name: string;
  // ユーザーのChatwork ID
  chatwork_id: string;
  // ユーザーの会社ID
  organization_id: number;
  // ユーザーの会社名
  organization_name: string;
  // ユーザーの部
  department: string;
  // ユーザーの役職
  title: string;
  // ユーザーが入力したカスタムURL
  url: string;
  // ユーザーの紹介
  introduction: string;
  // ユーザーのメアド
  mail: string;
  // ユーザーの会社電話番号
  tel_organization: string;
  // ユーザーの会社電話内線番号
  tel_extension: string;
  // ユーザーの携帯電話番号
  tel_mobile: string;
  // ユーザーのスカイプURL
  skype: string;
  // ユーザーのフェイスブックURL
  facebook: string;
  // ユーザーのX（ツイッター）のURL
  twitter: string;
  // ユーザーのアバター画像URL
  avatar_image_url: string;
  // ユーザーのログインに使用するのメアド
  login_mail: string;
}
```

#### `MyStatus`

ユーザーに割り当てられた未読メッセージとタスクの情報を含むオブジェクト。

```typescript
interface MyStatus {
  // 未読メッセージがある部屋数
  unread_room_num: number;
  // ユーザーに関する未読メッセージがある部屋の数
  mention_room_num: number;
  // ユーザーに割り当てられたタスクがある部屋の数
  mytask_room_num: number;
  // 未読メッセージ数
  unread_num: number;
  // ユーザーに関する未読メッセージ数
  mention_num: number;
  // ユーザーに割り当てられたタスク数
  mytask_num: number;
}
```

#### `TaskRoom`

タスクが割り当てられたチャットルームの詳細を含むオブジェクト。

```typescript
interface TaskRoom {
  // チャットルームID
  room_id: number;
  // チャットルーム名
  name: string;
  // チャットルームのアイコンのURL
  icon_path: string;
}
```

#### `MyTask`

現在の API トークンに関連付けられたユーザーに割り当てられたタスクの詳細を含むオブジェクト。
`Task`型から`account`プロパティを除き、`room`プロパティ(TaskRoom 型)を追加したもの。 `Task` は下記で定義。

```typescript
// Taskの定義は後述
type MyTask = Omit<Task, "account"> & { room: TaskRoom };
```

#### `Contact`

Chatwork コンタクトの詳細を含むオブジェクト。

```typescript
interface Contact {
  // コンタクトのアカウントID
  account_id: number;
  // コンタクトのルームID
  room_id: number;
  // コンタクトの名前
  name: string;
  // コンタクトのChatwork ID
  chatwork_id: string;
  // コンタクトの会社ID
  organization_id: number;
  // コンタクトの会社名
  organization_name: string;
  // コンタクトの部
  department: string;
  // コンタクトのアイコンのURL
  avatar_image_url: string;
}
```

#### `RoomInfo`

チャットルームの情報を含むオブジェクト。

```typescript
interface RoomInfo {
  // ルームID
  room_id: number;
  // ルーム名
  name: string;
  // ルームタイプ ('my', 'direct', 'group')
  type: "my" | "direct" | "group";
  // ユーザーのルームロール ('admin', 'member', 'readonly')
  role: "admin" | "member" | "readonly";
  // 固定されているか
  sticky: boolean;
  // 未読数
  unread_num: number;
  // メンション数
  mention_num: number;
  // 自分のタスク数
  mytask_num: number;
  // メッセージ数
  message_num: number;
  // ファイル数
  file_num: number;
  // タスク数
  task_num: number;
  // アイコンのパス
  icon_path: string;
  // 最終更新時間
  last_update_time: number;
}
```

#### `RoomsPostResponse`

`postRooms` 関数のレスポンス。

```typescript
interface RoomsPostResponse {
  // 新しく作成されたルームID
  room_id: number;
}
```

#### `RoomInfoWithDescription`

`RoomInfo` に説明を追加したオブジェクト。

```typescript
{
  // ルームID
  room_id: number;
  // ルーム名
  name: string;
  // ルームタイプ ('my', 'direct', 'group')
  type: "my" | "direct" | "group";
  // ユーザーのルームロール ('admin', 'member', 'readonly')
  role: "admin" | "member" | "readonly";
  // 固定されているか
  sticky: boolean;
  // 未読数
  unread_num: number;
  // メンション数
  mention_num: number;
  // 自分のタスク数
  mytask_num: number;
  // メッセージ数
  message_num: number;
  // ファイル数
  file_num: number;
  // タスク数
  task_num: number;
  // アイコンのパス
  icon_path: string;
  // 最終更新時間
  last_update_time: number;
  // ルームの概要
  description: string;
}
```

#### `RoomPutResponse`

`putRoom` 関数のレスポンス。

```typescript
interface RoomPutResponse {
  // 更新されたルームID
  room_id: number;
}
```

#### `RoomMember`

チャットルームのメンバー情報を含むオブジェクト。

```typescript
interface RoomMember {
  // アカウントID
  account_id: number;
  // ロール ('admin', 'member', 'readonly')
  role: "admin" | "member" | "readonly";
  // 名前
  name: string;
  // Chatwork ID
  chatwork_id: string;
  // 組織ID
  organization_id: number;
  // 組織名
  organization_name: string;
  // 部署
  department: string;
  // アバター画像URL
  avatar_image_url: string;
}
```

#### `RoomMembersPutResponse`

`putRoomMembers` 関数のレスポンス。

```typescript
interface RoomMembersPutResponse {
  // 管理者権限のユーザーのアカウントID一覧
  admin: number[];
  // メンバー権限のユーザーのアカウントID一覧
  member: number[];
  // 閲覧のみ権限のユーザーのアカウントID一覧
  readonly: number[];
}
```

#### `Message`

メッセージの情報を含むオブジェクト。

```typescript
interface Message {
  // メッセージID
  message_id: string;
  // アカウント情報
  account: AccountInfo;
  // メッセージ本文
  body: string;
  // 送信時間
  send_time: number;
  // 更新時間
  update_time: number;
}
```

#### `UpdatedMessage`

更新されたメッセージの情報を含むオブジェクト。
(メッセージ削除の場合は、削除されたメッセージの ID が返る)

```typescript
interface UpdatedMessage {
  // メッセージID
  message_id: string;
}
```

#### `RoomMessagesReadPutResponse`

`putRoomMessagesRead` 関数のレスポンス。

```typescript
interface RoomMessagesReadPutResponse {
  // 未読数
  unread_num: number;
  // メンション数
  mention_num: number;
}
```

#### `RoomMessagesUnreadPutResponse`

`putRoomMessagesUnread` 関数のレスポンス。

```typescript
interface RoomMessagesUnreadPutResponse {
  // 未読数
  unread_num: number;
  // メンション数
  mention_num: number;
}
```

#### `AccountInfo`

アカウント情報を含むオブジェクト。

```typescript
interface AccountInfo {
  // アカウントID
  account_id: number;
  // 名前
  name: string;
  // アバター画像URL
  avatar_image_url: string;
}
```

#### `Task`

タスクの情報を含むオブジェクト。

```typescript
interface Task {
  // タスクID
  task_id: number;
  // アカウント情報
  account: AccountInfo;
  // 割り当てたアカウント情報
  assigned_by_account: AccountInfo;
  // メッセージID
  message_id: string;
  // タスク本文
  body: string;
  // 期限
  limit_time: number;
  // ステータス ('open' or 'done')
  status: "open" | "done";
  // 期限のタイプ ('none', 'date', 'time')
  limit_type: "none" | "date" | "time";
}
```

#### `PostTasksResponse`

`postRoomTasks` 関数のレスポンス。

```typescript
interface PostTasksResponse {
  // 追加されたタスクIDのリスト
  task_ids: number[];
}
```

#### `File`

ファイルの情報を含むオブジェクト。

```typescript
interface File {
  // ファイルID
  file_id: number;
  // アカウント情報
  account: AccountInfo;
  // メッセージID
  message_id: string;
  // ファイル名
  filename: string;
  // ファイルサイズ
  filesize: number;
  // アップロード時間
  upload_time: number;
}
```

#### `UploadedFiles`

`postRoomFiles` のレスポンス。

```typescript
interface UploadedFiles {
  // アップロードされたファイルIDのリスト
  file_ids: string[];
}
```

#### `DownloadableFile`

ダウンロード URL を含むファイル情報。

```typescript
interface DownloadableFile {
  // ファイルID
  file_id: number;
  // アカウント情報
  account: AccountInfo;
  // メッセージID
  message_id: string;
  // ファイル名
  filename: string;
  // ファイルサイズ
  filesize: number;
  // アップロード時間
  upload_time: number;
  // ダウンロードURL
  download_url?: string;
}
```

#### `RoomInvitationLink`

チャットへの招待リンク情報を含むオブジェクト。

```typescript
interface RoomInvitationLink {
  // 公開設定
  public: boolean;
  // 招待リンクURL
  url: string;
  // 承認が必要か
  need_acceptance: boolean;
  // 説明文
  description: string;
}
```

#### `ContactRequest`

コンタクト承認依頼の情報を含むオブジェクト。

```typescript
interface ContactRequest {
  // リクエストID
  request_id: number;
  // アカウントID
  account_id: number;
  // メッセージ
  message: string;
  // 名前
  name: string;
  // Chatwork ID
  chatwork_id: string;
  // 組織ID
  organization_id: number;
  // 組織名
  organization_name: string;
  // 部署名
  department: string;
  // アバター画像URL
  avatar_image_url: string;
}
```

#### `ContactRequestApprovalResponse`

`putIncomingRequests` のレスポンス。

```typescript
interface ContactRequestApprovalResponse {
  // アカウントID
  account_id: number;
  // メッセージ
  message: string;
  // 名前
  name: string;
  // Chatwork ID
  chatwork_id: string;
  // 組織ID
  organization_id: number;
  // 組織名
  organization_name: string;
  // 部署名
  department: string;
  // アバター画像URL
  avatar_image_url: string;
}
```

#### `TaskIdResponse`

`putRoomTaskStatus` のレスポンス。

```typescript
interface TaskIdResponse {
  // タスクID
  task_id: number;
}
```

#### `TaskStatus`

```typescript
type TaskStatus = "open" | "done";
```

#### `TaskLimitType`

```typescript
type TaskLimitType = "none" | "date" | "time";
```

[Chatwork APIトークン]: https://www.chatwork.com/service/packages/chatwork/subpackages/api/token.php
