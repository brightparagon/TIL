##Node.js
######an asynchronous, event-driven, non-blocking I/O model that makes a server light and efficient

- #####The traditional way of making server program: multi-thread & synchronous
  In this system, every request from clients makes a thread. --> 1000 clients make 1000 threads in the server program
  and these threads are going onto the memory in the server whici is physically limited.
  so, this system is not desirable for the service where there are so many requests.
  
- #####Alternative: single-thread & asynchronous
  Unlike a multi-thread way, Node.js deals with requests as one single thread called 'Event Loop'(there are several threads in the baskside though).
  not waiting for the event that already was taken this system takes continuously other events.
  
  A simple flow of this system is like this
  1. the first event taken
  2. controll passed to the next event(second one)
  3. callback casted to the first event

- #####The limit of Node.js & a proper way of using it
  It is not efficient to use Node.js in the service where a large-sized data is usally dealt with.
  Because it would take a long time to return a callback to an event. The more requests would come, The worse it would be
  to the whole Node.js system.
  So, Node.js is appropriate and perfect for the service where there are many requests with a lightweight amount of data.
  
###Reference
* https://en.wikipedia.org/wiki/Node.js
* https://nodejs.org/en/about/
* http://www.nextree.co.kr/p7292/
