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

## Contributing

Found a bug? Have a feature request? Want to send fan mail? Open an issue or submit a pull request. We promise to read it, eventually.

## License

MIT License. Because sharing is caring.

Happy coding! 🎉
