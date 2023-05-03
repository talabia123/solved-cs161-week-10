Download Link: https://assignmentchef.com/product/solved-cs161-week-10
<br>
You will be writing a Library simulator. It will have three classes: Book, Patron and Library.  To make things a little simpler for you, I am supplying you with the three .hpp files. You will write the three implementation files.  You should not alter the provided .hpp files.




A couple of notes:

<ul>

 <li>The vector::erase() function lets you delete an element of a vector, shifting over all the elements after it.</li>

 <li>You’ll see in Book.hpp a line that says “class Patron;”. That is a forward declaration. It doesn’t say anything about the definition of the Paton class, but it promises the compiler that there will be a type named Patron.  The reason we don’t just say “#include Patron.hpp” is that both Book and Patron need to know about each other, but they can’t both #include the other because that would create a cyclic dependency.</li>

</ul>




Here are the .hpp files: <u>​</u><a href="https://oregonstate.instructure.com/courses/1568382/files/63473733/download?verifier=LrEB7X8tg0I5GSgdTOYvajbp0IbeokGdO9iu7LC7&amp;wrap=1">Book.hpp</a><u>​</u><a href="https://oregonstate.instructure.com/courses/1568382/files/63473733/download?verifier=LrEB7X8tg0I5GSgdTOYvajbp0IbeokGdO9iu7LC7&amp;wrap=1">,</a> ​<a href="https://oregonstate.instructure.com/courses/1568382/files/63473734/download?verifier=xu21Z8q9xgvrwr0hEEzifPsVZYaMLlxI0n7KijPU&amp;wrap=1">Patron.hpp</a>​ and ​<a href="https://oregonstate.instructure.com/courses/1568382/files/63473723/download?verifier=4TU5kpDKO7Sfk4kFLxzcPTuEDQsSDdUPhyoeuSjW&amp;wrap=1">Library.hpp</a>




Here are descriptions of the three classes:

Book:

<ul>

 <li>idCode – a unique identifier for a Book (think library bar code, not ISBN)</li>

 <li>title – cannot be assumed to be unique</li>

 <li>author – the idCode, title and author don’t need set methods, since they will never change after the object has been created, therefore these fields can be initialized directly within the constructor</li>

 <li>location – a Book can be either on the shelf, on the hold shelf, or checked out</li>

 <li>checkedOutBy – pointer to the Patron who has it checked out (if any)</li>

 <li>requestedBy – pointer to the Patron who has requested it (if any); a Book can only be requested by one Patron at a time</li>

 <li>dateCheckedOut – when a book is checked out, this will be set to the currentDate of the Library</li>

 <li>CHECK_OUT_LENGTH – constant that gives how long a Book can be checked out for</li>

 <li>constructor – takes an idCode, title and author; checkedOutBy and requestedBy should be initialized to NULL; a new Book should be on the shelf</li>

 <li>some get and set methods</li>

</ul>




Patron:

<ul>

 <li>idNum – a unique identifier for a Patron</li>

 <li>name – cannot be assumed to be unique</li>

 <li>checkedOutBooks – a vector of pointers to Books that Patron currently has checkedOut</li>

 <li>fineAmount – how much the Patron owes the Library in late fines (measured in dollars); this is allowed to go negative</li>

 <li>a constructor that takes an idNum and name and initializes fineAmount to zero</li>

 <li>some get and set methods</li>

 <li>addBook – adds the specified Book to checkedOutBooks</li>

 <li>removeBook – removes the specified Book from checkedOutBooks</li>

 <li>amendFine – a positive argument increases the fineAmount, a negative one decreases it</li>

</ul>




Library:

<ul>

 <li>holdings – a vector of pointers to Books in the Library</li>

 <li>members – a vector of pointers to Patrons in the Library</li>

 <li>currentDate – stores the current date represented as an integer number of “days” since the Library object was created</li>

 <li>a constructor that initializes the currentDate to zero</li>

 <li>addBook – adds the parameter to holdings</li>

 <li>addPatron – adds the parameter to members</li>

 <li>getBook – returns a pointer to the Book corresponding to the ID parameter, or NULL if no such Book is in the holdings</li>

 <li>getPatron – returns a pointer to the Patron corresponding to the ID parameter, or NULL if no such Patron is a member</li>

 <li>checkOutBook

  <ul>

   <li>if the specified Book is not in the Library, return “book not found”</li>

  </ul></li>

</ul>

○       if the specified Patron is not in the Library, return “patron not found”

○   if the specified Book is already checked out, return “book already checked out”

○   if the specified Book is on hold by another Patron, return “book on hold by other patron”

○   otherwise update the Book’s checkedOutBy, dateCheckedOut and Location; if the Book was on hold for this Patron, update requestedBy; update the Patron’s checkedOutBooks; return “check out successful”

<ul>

 <li>returnBook

  <ul>

   <li>if the specified Book is not in the Library, return “book not found”</li>

  </ul></li>

</ul>

○   if the Book is not checked out, return “book already in library”

○   update the Patron’s checkedOutBooks; update the Book’s location depending on whether another Patron has requested it; update the

Book’s checkedOutBy; return “return successful”

<ul>

 <li>requestBook

  <ul>

   <li>if the specified Book is not in the Library, return “book not found”</li>

  </ul></li>

</ul>

○       if the specified Patron is not in the Library, return “patron not found”

○   if the specified Book is already requested, return “book already on hold”

○   update the Book’s requestedBy; if the Book is on the shelf, update its location to on hold; return “request successful”

<ul>

 <li>payFine

  <ul>

   <li>takes as a parameter the amount that is being paid (not the negative of that amount)</li>

  </ul></li>

</ul>

○       if the specified Patron is not in the Library, return “patron not found”

○        use amendFine to update the Patron’s fine; return “payment successful”

<ul>

 <li>incrementCurrentDate

  <ul>

   <li>increment current date; increase each Patron’s fines by 10 cents for each overdue Book they have checked out (using amendFine)</li>

  </ul></li>

</ul>

○   If a book is checked out on day 0, then on day 1, the patron has had it for 1 day.  On day 21, the patron has had it for 21 days, so it is still not overdue.  On day 22, the book is overdue and fines will be charged.

<ul>

 <li><strong>be careful – a Book can be on request without its location being the hold shelf</strong> (if another Patron has it checked out);</li>

</ul>




One <strong>limited</strong>​ example of how your classes might be used is:​

Book b1(“123”, “War and Peace”, “Tolstoy”);

Book b2(“234”, “Moby Dick”, “Melville”);

Book b3(“345”, “Phantom Tollbooth”, “Juster”);

Patron p1(“abc”, “Felicity”);

Patron p2(“bcd”, “Waldo”);

Library lib;  lib.addBook(&amp;b1);  lib.addBook(&amp;b2);  lib.addBook(&amp;b3);  lib.addPatron(&amp;p1);  lib.addPatron(&amp;p2);  lib.checkOutBook(“bcd”, “234”);  for (int i=0; i&lt;7; i++)  lib.incrementCurrentDate();  lib.checkOutBook(“bcd”, “123”);  lib.checkOutBook(“abc”, “345”);  for (int i=0; i&lt;24; i++)  lib.incrementCurrentDate();  lib.payFine(“bcd”, 0.4);      double p1Fine = p1.getFineAmount();      double p2Fine = p2.getFineAmount();

This example obviously doesn’t include all of the functions described above.  You are responsible for testing <strong>all</strong>​ ​ of the required functions to make sure they operate as specified.





