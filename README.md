# Project Name
> Stomp-Book-Club

## Table of contents
* [General info](#general-info)
* [Technologies](#technologies)
* [Launch](#Launch)
* [Inspiration](#inspiration)
* [Goals](#Goals)
* [Contact](#contact)

## General info
A book club, in which users are able to signup for reading clubs and borrow books from each other. The server side is written in java, and it include the users management. In addition the server supports both thread-per-client and reactor. The client side is written in C++, and it include all the request from the users like: login, logut, borrow and more.



## Technologies
* Java - 8 Or 11
* Maven - version 3.6.3
* Reactor
* C++
* MakeFile
* Boost

## Launch
Open cmd\terminal in the project directory and run the next commend:</br>
### Server - Both Linux and Windows
#### Compile
> mvn compile </br>
#### Run
> Thread per client server: mvn exec:java -Dexec.mainClass="bgu.spl.net.impl.stomp.StompServer" -Dexec.args="port tpc </br>
> Reactor server: mvn exec:java -Dexec.mainClass="bgu.spl.net.impl.stomp.StompServer" -
Dexec.args="port reactor
### Client - Linux
Make sure that boost is installed.
#### Compile
> make </br>
#### Run
> ./client
### Client - Windows
Make sure that boost is installed.
#### Compile
> mvn compile </br>
#### Build

#### Run
> client.exe

## Run Examples
First run the Server with port number and and decided to use tpc or reactor. Then you will see The Server is on, and after that you can run the client, and give commands from there.

#### Input explanation
program would accept any of the next input text below from the client side:
* Login Command
  * Structure: login {host:port} {username} {password}
  * For this command a CONNECT frame is sent to the server.
  * You can assume that username and password contain only English and numeric The possible outputs the client can have for this command:
    * Socket error: connection error. In this case the output should be “Could not connect to
server”.
    * New user: If the server connection was successful and the server doesn’t find the
username, then a new user is created, and the password is saved for that user. Then the
server sends a CONNECTED frame to the client and the client will print "Login
successful”.
    * User is already logged in: If the user is already logged in, then the server will respond
with a STOMP error frame indicating the reason – the output in this case should be
“User already logged in”.
    * Wrong password: If the user exists and the password doesn’t match the saved
password, the server will send back an appropriate ERROR frame indicating the reason -
the output in this case should be “Wrong password”.
    * User exists: If the server connection was successful, the server will check if the user
exists in the users list, and if the password matches, also the server will check that the
user does not have an active connection already. In case these tests are OK, the server
sends back a CONNECTED frame and the client will print to the screen "Login
successful.”.
* Join Genre Reading Club Command
  * Structure: join {genre}
  * For this command a SUBSCRIBE frame is sent to the {genre} topic.
  * As a result, a RECIEPT will be returned to the client. A message “Joined club {genre}” will be
displayed to the screen.
* Exit Genre Reading Club Command
  * Structure: exit {genre}
  * For this command a UNSUBSCRIBE frame is sent to the {genre} topic.
  * As a result, a RECIEPT will be returned to the client. A message “Exited club {genre}” will be
displayed to the screen.
* Add Book Command
  * Structure: add {genre} {book name}
  * For this command a SEND frame is sent to the topic {genre} with the content: “{user} has added
the book {book name}
  * The book will be added to the client inventory.
  * The inventory is per genre, no book is multi genre.
* Borrow Book Command
  * Structure: borrow {genre} {book name}
  * For this command a SEND frame is sent to the topic {genre} with the “{user} wish to borrow
{book name}“ in the content.
  * The server distribute the msg to all users subscribed to the {genre}, if one of them holds the book
in his stock, he will send a SEND frame to the topic {genre}, with “{username} has {book name}”
as content.
  * If some one has the requested book, another SEND frame will be sent to the {genre} topic, with
"Taking {book name} from {book owner username}", this will result in the book adding up to the
original (the borrower) user inventory, and being removed from the lender inventory.
  * Transitive borrowing is allowed (I.e. Bob borrows from John which borrowed from Alice).
  * If multiple users has a book, the borrower will take from the first one only (according to msg
arrival order).
  * This command has multiple frames involved.
* Return Book Command
  * Structure: return {genre} {book name}
  * For this command a SEND frame is sent to {genre} topic with the content “Returning {book name}
to {book lender}”.
  * This will result in removing the book from the borrower inventory, and adding it back to the
lender.
  * If a book has been double borrowed, it need to be returned in the correct order.
* Genre Book Status Command
  * Structure: status {genre}
  * For this command a SEND frame is sent to the {genre} topic with "book status” in the body.
  * All the subscribed users will send a SEND frame, each with its current inventory, each book
seperated by a comma (,), and the name (example below).
* Logout Command
  * Structure: logout
  * This command tells the client that the user wants to log out from the library. The client will send
a DISCONNECT to the server.
  * The server will reply with a RECEIPT frame.
  * The logout command, removes the current user from all the topics.
  * Once the client receives the RECEIPT frame, it should close the socket and await further user
commands.
#### Output explanation
You have Output file provided to you in output folder as an example to what should be expected.
the folder file in which the Output file resieds in have the input needed to receive this expect output.

## Inspiration
As part of our System Programing course we received this project as an assignment.

## Goals
Practice communication by implementing a program that support client side and server side, using a stomp protocol to communicate. In addition support both thread per client and reactor in the server.

## Contact
Created by [Itamar Lederman](https://github.com/Itamarled/) & [Shimi Nagar](https://github.com/Shimonna394)