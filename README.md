# 🎟️ GoTickets - The Go-To Ticket Booking CLI! 🎟️

Welcome to **GoTickets**, the snazziest CLI application for booking tickets that you'll ever build while learning Golang! 🚀

![Gopher](https://golang.org/doc/gopher/frontpage.png)

## Why Go? Why Tickets? Why Not?

Ever wondered why Go was even developed? Or why you'd want to build a ticket booking system? Well, neither did we, but here we are, having a blast doing both!

## What’s This About?

In this epic adventure, you’ll master Golang by building a simple yet (over)ambitious ticket booking CLI application. Get ready to dive into the world of Go, where concurrency is king and the syntax is leaner than a cat on a diet.

## Features

- **Book Tickets**: Secure your spot at the imaginary Go Conference!
- **Validate Input**: Because booking tickets with invalid data is so 2023.
- **Concurrency**: Feel the power of Go’s goroutines as tickets fly into your email inbox (metaphorically speaking).
- **Error Messages**: Polite reminders that you’ve messed up your input (but in a nice way).

## Installation

Clone the repo, install Go, and you're halfway to being a Go guru!

```bash
git clone https://github.com/mysticalien/GoTickets.git
cd GoTickets
go mod tidy
```

## Usage

Fire up your terminal, put on your best ticket-booking hat, and run:

```bash
go run .
```

Then follow the prompts to book your tickets. It’s like Ticketmaster, but without the service fees.

## Code Breakdown

### Main Go File (`main.go`)

This is where the magic happens:

- **greetUsers**: Welcomes you like the VIP you are.
- **getUserInput**: Grabs your deets (first name, last name, email, and number of tickets).
- **bookTicket**: Books those sweet tickets and updates the remaining count.
- **sendTicket**: Sends you a virtual ticket via the magic of concurrency.
- **getFirstNames**: Because we all want to know who else is coming.

### Helper Go File (`helper.go`)

A little helper for all your validation needs:

- **ValidateUserInput**: Ensures your name isn’t too short, your email has an @, and you’re not trying to book more tickets than we have.

## The Code

**main.go**

```go
package main

import (
    "booking-app/helper"
    "fmt"
    "sync"
    "time"
)

const conferenceTickets int = 50

var conferenceName = "Go Conference"
var remainingTickets uint = 50
var bookings = make([]UserData, 0)

type UserData struct {
    firstName       string
    lastName        string
    email           string
    numberOfTickets uint
}

var wg = sync.WaitGroup{}

func main() {
    greetUsers()
    firstName, lastName, email, userTickets := getUserInput()
    isValidName, isValidEmail, isValidTicketNumber := helper.ValidateUserInput(firstName, lastName, email, userTickets, remainingTickets)

    if isValidName && isValidEmail && isValidTicketNumber {
        bookTicket(userTickets, firstName, lastName, email)
        wg.Add(1)
        go sendTicket(userTickets, firstName, lastName, email)
        firstNames := getFirstNames()
        fmt.Printf("The first names of bookings are: %v\n", firstNames)

        if remainingTickets == 0 {
            fmt.Println("Our conference is booked out. Come back next year.")
        }
    } else {
        if !isValidName {
            fmt.Println("First name or last name you entered is too short")
        }
        if !isValidEmail {
            fmt.Println("Email address you entered doesn't contain @ sign")
        }
        if !isValidTicketNumber {
            fmt.Println("Number of tickets you entered is invalid")
        }
    }
    wg.Wait()
}

func greetUsers() {
    fmt.Printf("Welcome to %v booking application\n", conferenceName)
    fmt.Printf("We have total of %v tickets and %v are still available.\n", conferenceTickets, remainingTickets)
    fmt.Println("Get your tickets here to attend")
}

func getFirstNames() []string {
    firstNames := []string{}
    for _, booking := range bookings {
        firstNames = append(firstNames, booking.firstName)
    }
    return firstNames
}

func getUserInput() (string, string, string, uint) {
    var firstName, lastName, email string
    var userTickets uint

    fmt.Println("Enter your first name: ")
    fmt.Scan(&firstName)

    fmt.Println("Enter your last name: ")
    fmt.Scan(&lastName)

    fmt.Println("Enter your email address: ")
    fmt.Scan(&email)

    fmt.Println("Enter number of tickets: ")
    fmt.Scan(&userTickets)

    return firstName, lastName, email, userTickets
}

func bookTicket(userTickets uint, firstName, lastName, email string) {
    remainingTickets -= userTickets

    var userData = UserData{
        firstName:       firstName,
        lastName:        lastName,
        email:           email,
        numberOfTickets: userTickets,
    }

    bookings = append(bookings, userData)

    fmt.Printf("List of bookings is %v\n", bookings)
    fmt.Printf("Thank you %v %v for booking %v tickets. You will receive a confirmation email at %v\n", firstName, lastName, userTickets, email)
    fmt.Printf("%v tickets remaining for %v\n", remainingTickets, conferenceName)
}

func sendTicket(userTickets uint, firstName, lastName, email string) {
    time.Sleep(10 * time.Second)
    var ticket = fmt.Sprintf("%v tickets for %v %v", userTickets, firstName, lastName)
    fmt.Println("###############")
    fmt.Printf("Sending ticket:\n %v \nto email address %v\n", ticket, email)
    fmt.Println("###############")
    wg.Done()
}
```

**helper.go**

```go
package helper

import "strings"

func ValidateUserInput(firstName, lastName, email string, userTickets, remainingTickets uint) (bool, bool, bool) {
    isValidName := len(firstName) >= 2 && len(lastName) >= 2
    isValidEmail := strings.Contains(email, "@")
    isValidTicketNumber := userTickets > 0 && userTickets <= remainingTickets
    return isValidName, isValidEmail, isValidTicketNumber
}
```

## Contributing

Found a bug? Have a feature request? Want to send fan mail? Open an issue or submit a pull request. We promise to read it, eventually.

## License

MIT License. Because sharing is caring.

Happy coding! 🎉
