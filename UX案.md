mermaid
flowchart TD
    %% メイン画面と基本遷移
    Books[書籍一覧] --> Detail[書籍詳細]
    
    %% 未ログイン時の動線（「、、、」を排除し、アクセス制限の挙動を明確化）
    Guest[未ログインで認証必須画面へアクセス] --> Login[ログイン画面]
    Detail -->|レビュー投稿のログイン案内| Login
    Books -->|共通ナビ・未ログイン時| Register[会員登録画面]
    Books -->|共通ナビ・未ログイン時| Login
    
    %% 会員登録・ログインの相互遷移とエラーハンドリング
    Register -->|ログインへ| Login
    Login -->|会員登録へ| Register
    Register -->|入力エラー| Register
    Login -->|入力・認証エラー| Login
    
    %% 認証成功後の条件分岐（元の保護画面へのリダイレクト）
    Register -->|登録成功・ログイン状態| Books
    Login -->|ログイン成功| Destination{元の保護画面があるか}
    Destination -->|あり| Protected[元の認証必須GET画面]
    Destination -->|なし| Books
    
    %% 書籍登録・編集・削除の機能
    Books -->|ログイン済み| Create[書籍登録]
    Create -->|登録成功| Detail
    Create -->|キャンセル| Books
    Detail -->|登録者のみ| Edit[書籍編集]
    Edit -->|更新成功・キャンセル| Detail
    Detail -->|書籍削除成功| Books
    
    %% レビュー機能
    Detail -->|レビュー投稿・削除成功| Detail
    Detail -->|投稿者のみ| ReviewEdit[レビュー編集]
    ReviewEdit -->|更新成功・キャンセル| Detail
    
    %% お気に入り機能
    Detail -->|ログイン済み・ハートボタン| FavoriteAction([お気に入り登録・解除の操作])
    FavoriteAction -->|処理成功・同じ詳細へ| Detail
    Books -->|共通ナビ・ログイン済み| Favorites[お気に入り一覧]
    Favorites -->|書籍を選択| Detail
    Favorites -->|解除成功| Favorites
    
    %% 共通ナビゲーション（ランキング・ジャンル）
    Books -->|共通ナビ| Ranking[ランキング]
    Ranking --> Detail
    Books -->|共通ナビ・ログイン済み| Genres[ジャンル一覧]
    Genres --> GenreBooks[ジャンル別書籍一覧]
    GenreBooks --> Detail
    Genres --> GenreForm[ジャンル登録・編集]
    GenreForm -->|保存成功・キャンセル| Genres