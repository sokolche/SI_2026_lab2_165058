# SI_2026_lab2_165058
Iva Sokolovska 165058


2. 
Control Flow Graph за searchBookByTitle
                    ┌─────────┐
                    │  START  │
                    └────┬────┘
                         │
                         v
              ┌─────────────────────┐
              │ title.isEmpty()?    │
              └──────┬────────┬─────┘
                   true       false
                    │          │
                    v          v
        ┌──────────────────┐   ┌─────────────────────────┐
        │ throw exception  │   │ results = new ArrayList │
        └────────┬─────────┘   └───────────┬─────────────┘
                 │                         │
                 v                         v
              ┌─────┐              ┌─────────────────────┐
              │ END │              │ for each book       │
              └─────┘              └──────┬────────┬─────┘
                                      има │        │ нема
                                      книга       │ повеќе книги
                                           │        │
                                           v        v
                      ┌──────────────────────────┐ ┌─────────────────────┐
                      │ title matches AND        │ │ results.isEmpty()?  │
                      │ book is not borrowed?    │ └──────┬────────┬─────┘
                      └──────┬────────────┬──────┘     true       false
                           true          false          │          │
                            │              │            v          v
                            v              │   ┌─────────────┐ ┌──────────────┐
                   ┌────────────────┐      │   │ return null │ │ return results│
                   │ results.add()  │      │   └──────┬──────┘ └──────┬───────┘
                   └───────┬────────┘      │          │               │
                           │               │          v               v
                           └───────┬───────┘        ┌─────┐        ┌─────┐
                                   │                │ END │        │ END │
                                   v                └─────┘        └─────┘
                              назад на for


Control Flow Graph за borrowBook

                         ┌─────────┐
                         │  START  │
                         └────┬────┘
                              │
                              v
        ┌─────────────────────────────────────┐
        │ title.isEmpty() || author.isEmpty()?│
        └───────────────┬─────────────────────┘    
                 true   │   false               
                        │                   
        ┌───────────────┘
        v
┌──────────────────────────────────────┐
│ throw IllegalArgumentException        │
│ "Invalid search query"               │
└──────────────────┬───────────────────┘
                   │
                   v
                 ┌─────┐
                 │ END │
                 └─────┘

false од првиот if:
                              │
                              v
                 ┌─────────────────────┐
                 │ for each book       │
                 │ in books            │
                 └──────┬────────┬─────┘
                  има   │        │ нема повеќе
                  книга │        │ книги
                        │        │
                        v        v
 ┌──────────────────────────────────────┐
 │ title matches && author matches?     │
 └──────────────┬───────────────────────┘
          true  │ false
                │
                │
                v
      ┌─────────────────────┐
      │ !book.isBorrowed()? │
      └──────┬────────┬─────┘
          true       false
           │           │
           v           v
┌────────────────────┐  ┌──────────────────────────────┐
│ book.setBorrowed   │  │ throw RuntimeException        │
│ println success    │  │ "Book is already borrowed."  │
└─────────┬──────────┘  └──────────────┬───────────────┘
          │                            │
          v                            v
   ┌────────────┐                    ┌─────┐
   │ return     │                    │ END │
   └─────┬──────┘                    └─────┘
         │
         v
       ┌─────┐
       │ END │
       └─────┘


false од title matches && author matches:
                │
                v
          назад на for loop


кога for нема повеќе книги:
                        │
                        v
        ┌──────────────────────────────┐
        │ throw RuntimeException       │
        │ "Book not found"            │
        └──────────────┬───────────────┘
                       │
                       v
                     ┌─────┐
                     │ END │
                     └─────┘


3. Цикломатската комплексност на функцијата **searchBookByTitle** е 5, ако целиот услов со && се третира како еден decision point.

  Decision points:
  1. if (title.isEmpty())
  2. for (Book book:books)
  3. if  (book.setTitle()).equalsIgnoreCase(title) && !book.isBorrowed())
  4. if (results.isEmpty())

    па така V(G) = 4 + 1 = 5, 

    но ако условот на decision point 3 се третира како два decision points, тогаш цикломатска комплексност ќе биде
    V(G) = 5 + 1 = 6

  Цикломатска комплексност на функцијата **borrowBook** е 5, ако условите со && и || се третираат како еден decision point.

  Decision points:
  1. if (title.isEmpty() || author.isEmpty())
  2. for (Book book : books)
  3. if (book.getTitle().equalsIgnoreCase(title) && book.getAuthor().equalsIgnoreCase(author))
  4. 4. if (!book.isBorrowed())

  па така V(G) = 4 + 1 = 5,

  но ако условите на decision points 1 и 3 се третираат како два decision points, тогаш цикломатска комплексност ќе биде
    V(G) = 6 + 1 = 7


  
