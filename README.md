# VanillaUtilities

A collection of essential utilities for .NET developers that solve common real-world problems with clean, efficient code.

![NuGet Version](https://img.shields.io/nuget/v/VanillaUtilities?logo=nuget)
![GitHub License](https://img.shields.io/github/license/rrohankumawat/VanillaUtilities-Docs?logo=github)

## 📦 Installation

```bash
dotnet add package VanillaUtilities

```

🛠 Utilities Overview

🔐 JWT Utilities

```bash
// Generate JWT tokens
string GenerateAccessToken(string secretKey, string issuer, string audience, 
                         IEnumerable<Claim> claims, DateTime? expires = null)

// Generate secure refresh tokens  
string GenerateRefreshToken(int size = 32)

// Validate tokens
ClaimsPrincipal? ValidateToken(string token, string secretKey, 
                             string issuer, string audience)


var token = JwtUtilities.GenerateAccessToken(
    secretKey: "your-256-bit-secret",
    issuer: "your-app",
    audience: "your-api",
    claims: userClaims);                  
```

📧 SMTP Email Utilities

```bash
// Send emails with attachments
Task SendEmailAsync(
    SmtpConfig config,
    string subject,
    string body,
    IEnumerable<string> toAddresses,
    IEnumerable<EmailAttachment>? attachments = null,
    IEnumerable<string>? ccAddresses = null,
    IEnumerable<string>? bccAddresses = null,
    bool isBodyHtml = true)


public class SmtpConfig {
    public string Host { get; set; }
    public int Port { get; set; } = 587;
    public bool UseSsl { get; set; } = true;
    // ... other properties
}

```

📊 Excel Utilities

```bash
// Read/write Excel files
byte[] CreateExcelFromDataTable(DataTable dataTable, string sheetName = "Sheet1")
DataTable ReadExcelToDataTable(byte[] fileBytes, int sheetNumber = 1)

// CSV handling
List<T> ReadCsv<T>(Stream stream, bool hasHeader = true)
void WriteCsv<T>(IEnumerable<T> items, Stream stream, bool writeHeader = true)

```

📅 DateTime Utilities

```bash

// Date calculations
int CalculateAge(DateTime birthDate, DateTime? referenceDate = null)
DateTime AddBusinessDays(DateTime date, int days, IEnumerable<DateTime>? holidays = null)

// Week boundaries
DateTime GetStartOfWeek(DateTime date, DayOfWeek startOfWeek = DayOfWeek.Monday)
DateTime GetEndOfWeek(DateTime date, DayOfWeek startOfWeek = DayOfWeek.Monday)

```

🧵 String Utilities

```bash

// String transformations
string GenerateSlug(this string phrase)
string ToTitleCase(this string value)
string RemoveSpecialCharacters(this string input)

// Validation
bool IsNullOrEmpty(this string? value)
bool IsNullOrWhiteSpace(this string? value)

```

🎲 Random Generation

```bash
// Secure random values
int GenerateInt(int minValue = int.MinValue, int maxValue = int.MaxValue)
string GenerateSecurePassword(int length = 16)
string GenerateString(int length, string? allowedChars = null)

```

📦 Collection Utilities

```bash

// Collection operations
IEnumerable<T> Shuffle<T>(this IEnumerable<T> source)
IEnumerable<IEnumerable<T>> Batch<T>(this IEnumerable<T> source, int size)
DataTable ToDataTable<T>(this IEnumerable<T> items)

```

🔧 Configuration

```bash

JWT Configuration

"Jwt": {
  "Secret": "your-256-bit-secret",
  "Issuer": "your-app",
  "Audience": "your-api",
  "ExpiryMinutes": 15
}


SMTP Configuration

"Smtp": {
  "Host": "smtp.example.com",
  "Port": 587,
  "Username": "your@email.com",
  "Password": "your-password",
  "FromEmail": "noreply@example.com",
  "FromName": "Your App"
}

```

🚀 Quick Start

1. Install the package:
```bash
    dotnet add package VanillaUtilities
```
2. Import the namespace:
```bash
    using VanillaUtilities;
```
3. Use the utilities:
```bash
    // JWT Example
    var token = JwtUtilities.GenerateAccessToken(...);

    // Email Example
    await SmtpUtility.SendEmailAsync(...);        
```



📬 Contact

For questions or support:

Email: rohankumawat39@gmail.com

GitHub Issues: github.com/rrohankumawat/VanillaUtilities-Docs/issues
