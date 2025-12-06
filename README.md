# Library App

## Description

Library App is a .NET 8.0 console application that manages library patrons, books, and loans. The application provides a user-friendly interface for searching patrons, viewing their loan details, renewing memberships, extending loan due dates, and marking books as returned. Data is persisted using JSON files for simple, file-based storage.

## Project Structure

```
AccelerateDevGitHubCopilot/
├── src/
│   ├── Library.ApplicationCore/
│   │   ├── Library.ApplicationCore.csproj
│   │   ├── Entities/
│   │   │   ├── Author.cs
│   │   │   ├── Book.cs
│   │   │   ├── BookItem.cs
│   │   │   ├── Loan.cs
│   │   │   └── Patron.cs
│   │   ├── Enums/
│   │   │   ├── EnumHelper.cs
│   │   │   ├── LoanExtensionStatus.cs
│   │   │   ├── LoanReturnStatus.cs
│   │   │   └── MembershipRenewalStatus.cs
│   │   ├── Interfaces/
│   │   │   ├── IPatronRepository.cs
│   │   │   ├── ILoanRepository.cs
│   │   │   ├── IPatronService.cs
│   │   │   └── ILoanService.cs
│   │   └── Services/
│   │       ├── PatronService.cs
│   │       └── LoanService.cs
│   ├── Library.Console/
│   │   ├── Library.Console.csproj
│   │   ├── Program.cs
│   │   ├── ConsoleApp.cs
│   │   ├── ConsoleState.cs
│   │   ├── CommonActions.cs
│   │   ├── appSettings.json
│   │   └── Json/
│   │       ├── Authors.json
│   │       ├── Books.json
│   │       ├── BookItems.json
│   │       ├── Patrons.json
│   │       └── Loans.json
│   └── Library.Infrastructure/
│       ├── Library.Infrastructure.csproj
│       └── Data/
│           ├── JsonData.cs
│           ├── JsonPatronRepository.cs
│           └── JsonLoanRepository.cs
└── tests/
    └── UnitTests/
        ├── UnitTests.csproj
        ├── LoanFactory.cs
        ├── PatronFactory.cs
        └── ApplicationCore/
            ├── LoanService/
            │   ├── ExtendLoan.cs
            │   └── ReturnLoan.cs
            └── PatronService/
                └── RenewMembership.cs
```

## Key Classes and Interfaces

### Core Entities

- **Patron** - Represents a library member with membership dates and associated loans
- **Loan** - Represents a book loan with loan date, due date, and return date
- **Book** - Represents a book title with author and genre information
- **BookItem** - Represents a physical copy of a book
- **Author** - Represents an author of a book

### Services

- **PatronService** - Implements patron membership renewal with validation
- **LoanService** - Handles loan extensions and returns

### Repositories

- **JsonPatronRepository** - Implements IPatronRepository for patron data access
- **JsonLoanRepository** - Implements ILoanRepository for loan data access
- **JsonData** - Singleton service managing JSON file I/O and in-memory data population

### User Interface

- **ConsoleApp** - Main console application with state machine navigation
- **ConsoleState** - Enum defining application states (PatronSearch, PatronSearchResults, PatronDetails, LoanDetails, Quit)

## Usage

### Building the Project

```bash
dotnet build
```

### Running the Application

```bash
dotnet run --project src/Library.Console/Library.Console.csproj
```

### Running Unit Tests

```bash
dotnet test tests/UnitTests/UnitTests.csproj
```

### Application Flow

1. **Search for Patrons** - Enter a patron name to search the library database
2. **View Patron Details** - Select a patron to see their information and active loans
3. **Renew Membership** - Extend a patron's membership expiration date (if valid)
4. **Manage Loans** - View individual loans and perform actions:
   - Extend the due date
   - Mark the book as returned
5. **Exit** - Quit the application

### Configuration

JSON file paths can be configured in appSettings.json:

```json
{
  "JsonPaths": {
    "Authors": "Json/Authors.json",
    "Books": "Json/Books.json",
    "BookItems": "Json/BookItems.json",
    "Patrons": "Json/Patrons.json",
    "Loans": "Json/Loans.json"
  }
}
```

## License

Unlicensed
