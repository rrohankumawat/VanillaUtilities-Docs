# VanillaUtilities

A collection of essential utilities for .NET developers that solve common real-world problems with clean, efficient code.

![NuGet Version](https://img.shields.io/nuget/v/VanillaUtilities?logo=nuget)
![GitHub License](https://img.shields.io/github/license/rrohankumawat/VanillaUtilities-Docs?logo=github)

## 📦 Installation

```bash
dotnet add package VanillaUtilities

```

## 🛠 Utilities Overview

**</>** API Versioning Extension

 API Versioning Utility for your VanillaUtilities package that supports multiple versioning strategies.

Program.cs
 ```bash

//1. URL Segment Versioning (Default in your setup)
services.AddApiVersioningUtility();

//2. Query String Versioning (If configured with VersioningScheme.QueryString)
services.AddApiVersioningUtility(versioningScheme: VersioningScheme.QueryString);

//3. Header Versioning (If configured with VersioningScheme.Header)
services.AddApiVersioningUtility(versioningScheme: VersioningScheme.Header);

//4. Media Type Versioning (If configured with VersioningScheme.MediaType)
services.AddApiVersioningUtility(versioningScheme: VersioningScheme.MediaType);

```

Use curl to test different versioning schemes:

```bash
# URL Segment
curl https://yourdomain.com/api/v1/products

# Query String
curl https://yourdomain.com/api/products?api-version=1.0

# Header
curl -H "x-api-version: 1.0" https://yourdomain.com/api/products

# Media Type
curl -H "Accept: application/json;v=1.0" https://yourdomain.com/api/products
```

🔐 JWT Utilities

```bash
// Generate JWT tokens
string GenerateJwtToken(string secretKey, string issuer, string audience, IEnumerable<Claim> claims, DateTime? expires = null)

// Generate secure refresh tokens
string GenerateRefreshToken(int size = 32)

// Validate tokens
ClaimsPrincipal? ValidateToken(string token, string secretKey, string issuer, string audience)


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

➡️ API Generic Responses

```bash

//Perfect Response


using VanillaUtilities;
using System.Net;

public IActionResult GetUser()
{
    ApiResponsesUtilities<string>.Data = "John Doe";
    ApiResponsesUtilities<string>.Message = "User retrieved successfully";
    ApiResponsesUtilities<string>.Status = HttpStatusCode.OK;
    ApiResponsesUtilities<string>.Success = true;

    return Ok(ApiResponsesUtilities<string>);
}



//Response with Errors



using VanillaUtilities;
using System.Net;

public IActionResult GetUser(int id)
{
    try
    {
        throw new Exception("User not found.");
    }
    catch (Exception ex)
    {
        ApiResponsesUtilities<string>.Data = null;
        ApiResponsesUtilities<string>.Message = "An error occurred";
        ApiResponsesUtilities<string>.Status = HttpStatusCode.NotFound;
        ApiResponsesUtilities<string>.Success = false;
        ApiResponsesUtilities<string>.Error = new CustomException(ex.Message, ex);

        return NotFound(ApiResponsesUtilities<string>);
    }
}


```


📁 File Utilities

```bash
// Read & Write All Texts from file
async Task<string> ReadAllTextAsync(string filePath, CancellationToken cancellationToken = default)
Task WriteAllTextAsync(string filePath, string content, CancellationToken cancellationToken = default)

//Zip and Folder Related Operations
CreateZipFromDirectory(string sourceDirectory, string destinationZipFilePath, bool overwrite = true)
ExtractZipToDirectory(string sourceZipFilePath, string destinationDirectory, bool overwrite = true)
GetDirectorySize(string path)
```

📊 Excel Utilities

```bash
// Read/write Excel files
byte[] CreateExcelFromDataTable(DataTable dataTable, string sheetName = "Sheet1")
DataTable ReadExcelToDataTable(byte[] fileBytes, int sheetNumber = 1)
byte[] CreateExcelFromObjects<T>(IEnumerable<T> items, string sheetName = "Sheet1", string? tableName = null)

// CSV handling
List<T> ReadCsv<T>(Stream stream, bool hasHeader = true)
void WriteCsv<T>(IEnumerable<T> items, Stream stream, bool writeHeader = true)

//Converts collections to DataTable
DataTable ToDataTable<T>(this IEnumerable<T> items)
```

📅 DateTime Utilities

```bash

// Date calculations
int CalculateAge(DateTime birthDate, DateTime? referenceDate = null)
DateTime AddBusinessDays(DateTime date, int days, IEnumerable<DateTime>? holidays = null)
bool IsBusinessDay(DateTime date, IEnumerable<DateTime>? holidays = null)

// Week boundaries
DateTime GetStartOfWeek(DateTime date, DayOfWeek startOfWeek = DayOfWeek.Monday)
DateTime GetEndOfWeek(DateTime date, DayOfWeek startOfWeek = DayOfWeek.Monday)

```

🧵 String Utilities

```bash

// String transformations
string Truncate(this string value, int maxLength)
string GenerateSlug(this string phrase)
string ToTitleCase(this string value)
string RemoveSpecialCharacters(this string input)
byte[] ToByteArray(this string value) => Encoding.UTF8.GetBytes(value)

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
Dictionary<TKey, TValue> ToDictionaryIgnoreDuplicates<TSource, TKey, TValue>(this IEnumerable<TSource> source, Func<TSource, TKey> keySelector, Func<TSource, TValue> valueSelector)
ForEach<T>(this IEnumerable<T> source, Action<T> action)
bool IsNullOrEmpty<T>(this IEnumerable<T>? collection)


```

✨ Validation Helpers

```bash
bool IsValidEmail(string email)
bool IsValidPhoneNumber(string phoneNumber)
bool IsStrongPassword(string password)
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

Suggestions & Feedbacks are appreciated:

Email: rohankumawat39@gmail.com

GitHub Issues: github.com/rrohankumawat/VanillaUtilities-Docs/issues
