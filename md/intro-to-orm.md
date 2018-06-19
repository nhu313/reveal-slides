#Intro to ORM(Object Relational Mapping)
-
-
# Relationship

1. One to One
2. One to Many
3. Many to Many

-
## One to One
- One book linked to one ISBN
- One ISBN per book

```java
@DatabaseTable(tableName = "books")
public class Book {

  @DatabaseField(generatedId = true)
  private int id;

  @DatabaseField(canBeNull = false, foreign = true)
  private ISBN isbn;
}
```

-
## One to one

```
CREATE TABLE `books`
   (`id` INTEGER AUTO_INCREMENT , `isbn_id` INTEGER,
    PRIMARY KEY (`id`));
```

-
## One to one - Create

```
//create ISBN first
ISBN isbn = new ISBN("134235454323");
isbnDao.create(isbn);

// now we can set the isbn on the book and create it
Book book = new Book("The Giver");
book.setISBN(isbn);

bookDao.create(book);
```

-
## One to one - Auto create


```java
@DatabaseTable(tableName = "books")
public class Book {

  @DatabaseField(generatedId = true)
  private int id;

  @DatabaseField(foreignAutoCreate = true, canBeNull = false, foreign = true)
  private ISBN isbn;
}
```

-
## One to one - Auto Create

```
ISBN isbn = new ISBN("134235454323");
Book book = new Book("The Giver");
book.setISBN(isbn);

bookDao.create(book);
```

-
## One to One - Retrieve

```
Book book = bookDao.queryForId(bookId);
book.getISBN().getID(); //only set the id, nothing else

// have to refresh in order for the other fields to be populated
isbnDao.refresh(book.getISBN());
```
-

## One to One - Auto Retrieve


```java
@DatabaseTable(tableName = "books")
public class Book {

  @DatabaseField(generatedId = true)
  private int id;

  @DatabaseField(foreignAutoRefresh = true, canBeNull = false, foreign = true)
  private ISBN isbn;
}
```

```
Book book = bookDao.queryForId(bookId);
book.getISBN().getNumber();
```
-
-

## One to Many
Publisher has published many books

```java
@DatabaseTable(tableName = "books")
public class Book {

  @DatabaseField(generatedId = true)
  private int id;

  @DatabaseField(canBeNull = false, foreign = true)
  private Publisher publisher;
}
```

-
## One to Many

```java
public class Publisher {
  @ForeignCollectionField(eager = false)
  ForeignCollection<Book> books;
}

```
-
-
## Many to Many
Book can have many authors
Author can have many books

```java
@DatabaseTable(tableName = "books_authors")
public class BookAuthor {

    @DatabaseField(generatedId = true)
    private long id;

    @DatabaseField(canBeNull = false, foreign = true, foreignAutoCreate = true, foreignAutoRefresh = true)
    protected Book book;

    @DatabaseField(foreignAutoCreate = true, foreign = true, canBeNull = false, foreignAutoRefresh = true)
    protected Author author;
}
```

-
## Many to Many

```java
@DatabaseTable(tableName = "books")
public class Book {
    @DatabaseField
    private String title;

    @DatabaseField(generatedId = true)
    private int id;

    @ForeignCollectionField(eager = false)
    private ForeignCollection<BookAuthor> bookAuthors;
}
```

-
## Many to Many

```java
@DatabaseTable(tableName = "authors")
public class Author {

    @DatabaseField(generatedId = true)
    private int id;

    @DatabaseField
    private String name;

    @ForeignCollectionField(eager = true)
    private ForeignCollection<BookAuthor> bookAuthors;
}
```
