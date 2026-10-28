```mermaid
flowchart TD
    Books[書籍一覧] --> Detail[書籍詳細]
    Books --> Create[書籍登録]
    Create -->|登録成功| Detail
    Create -->|キャンセル| Books
    Detail --> Edit[書籍編集]
    Edit -->|更新成功・キャンセル| Detail
    Detail -->|書籍削除成功| Books
    Detail -->|レビュー投稿・削除成功| Detail
    Detail --> ReviewEdit[レビュー編集]
    ReviewEdit -->|更新成功・キャンセル| Detail
    Favorites[お気に入り一覧] --> Detail
    Ranking[ランキング] --> Detail
    Genres[ジャンル一覧] --> GenreBooks[ジャンル別書籍一覧]
    GenreBooks --> Detail
    Genres --> GenreForm[ジャンル登録・編集]
    GenreForm -->|保存成功・キャンセル| Genres
```