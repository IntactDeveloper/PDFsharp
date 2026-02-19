# PDFsharp & MigraDoc Repository - Main Functionality Overview

## Introduction

This repository contains **PDFsharp** and **MigraDoc**, two powerful .NET libraries for creating and manipulating PDF documents. Both libraries are developed by empira Software GmbH and are released under the MIT License, making them free for commercial and non-commercial use.

**Current Version:** 6.2.2  
**Published:** 2025-09-22  
**Targets:** .NET 6, .NET 8, and .NET Standard 2.0  
**License:** MIT License

## Main Components

### 1. PDFsharp - PDF Creation and Manipulation Library

**PDFsharp** is a .NET library that enables developers to create, read, and modify PDF documents programmatically without requiring Adobe Acrobat or any other PDF software.

#### Key Features:

- **Create PDF Documents from Scratch**: Generate new PDF files with complete control over content and layout
- **Modify Existing PDFs**: Read and modify existing PDF documents
- **Drawing API**: Provides a comprehensive graphics API (`XGraphics`) for drawing:
  - Text with various fonts and styles
  - Shapes (lines, rectangles, ellipses, polygons)
  - Images (PNG, JPEG, etc.)
  - Paths and curves
- **Advanced PDF Features**:
  - PDF forms and AcroForms
  - Digital signatures
  - Encryption and security
  - Annotations and actions
  - PDF/A compliance support
  - Barcode generation
  - Charting capabilities
- **Multi-Platform Support**:
  - Core build (cross-platform)
  - GDI+ build (Windows-specific)
  - WPF build (Windows-specific)

#### PDFsharp Use Case Example:
```csharp
// Create a new PDF document
var document = new PdfDocument();
document.Info.Title = "Created with PDFsharp";

// Add a page
var page = document.AddPage();

// Get graphics object for drawing
var gfx = XGraphics.FromPdfPage(page);

// Draw shapes and text
gfx.DrawLine(XPens.Red, 0, 0, page.Width, page.Height);
var font = new XFont("Times New Roman", 20, XFontStyleEx.BoldItalic);
gfx.DrawString("Hello, PDFsharp!", font, XBrushes.Black, 
    new XRect(0, 0, page.Width, page.Height), XStringFormats.Center);

// Save the document
document.Save("output.pdf");
```

### 2. MigraDoc - Document Creation Framework

**MigraDoc** is a high-level document creation framework that sits on top of PDFsharp. It provides a document object model for creating formatted documents that can be rendered to PDF, RTF, or other formats.

#### Key Features:

- **Document Object Model**: Create documents using a structured object model rather than low-level drawing commands
- **Automatic Layout**: MigraDoc handles text flow, page breaks, and formatting automatically
- **Rich Text Support**: 
  - Paragraphs with various formatting options
  - Multiple font styles, colors, and sizes
  - Tables with sophisticated layout options
  - Headers and footers
  - Lists (numbered and bulleted)
  - Images and shapes
- **Sections and Styles**: Define document structure with sections and reusable styles
- **Charts and Diagrams**: Built-in charting capabilities
- **Fields**: Dynamic content like dates, page numbers, and calculated values
- **Multiple Output Formats**: 
  - PDF rendering via PDFsharp
  - RTF (Rich Text Format)

#### MigraDoc Use Case Example:
```csharp
// Create a MigraDoc document
Document document = new Document();

// Add a section
Section section = document.AddSection();

// Add formatted content
Paragraph paragraph = section.AddParagraph();
paragraph.Format.Font.Color = Colors.DarkBlue;
paragraph.AddFormattedText("Hello, World!", TextFormat.Bold);

// Add footer with date field
HeaderFooter footer = section.Footers.Primary;
paragraph = footer.AddParagraph();
paragraph.Add(new DateField { Format = "yyyy/MM/dd HH:mm:ss" });

// Render to PDF
var pdfRenderer = new PdfDocumentRenderer()
{
    Document = document
};
pdfRenderer.RenderDocument();
pdfRenderer.PdfDocument.Save("output.pdf");
```

## Repository Structure

```
PDFsharp/
├── src/
│   ├── foundation/
│   │   ├── src/
│   │   │   ├── PDFsharp/         # PDFsharp library source code
│   │   │   │   ├── src/
│   │   │   │   │   ├── PdfSharp/              # Core build
│   │   │   │   │   ├── PdfSharp-gdi/          # GDI+ build
│   │   │   │   │   ├── PdfSharp-wpf/          # WPF build
│   │   │   │   │   ├── PdfSharp.BarCodes/     # Barcode support
│   │   │   │   │   ├── PdfSharp.Charting/     # Charting capabilities
│   │   │   │   │   └── PdfSharp.Cryptography/ # Security features
│   │   │   │   ├── tests/         # Unit tests
│   │   │   │   └── features/      # Feature tests
│   │   │   ├── MigraDoc/          # MigraDoc library source code
│   │   │   │   ├── src/
│   │   │   │   │   ├── MigraDoc.DocumentObjectModel/ # Document model
│   │   │   │   │   ├── MigraDoc.Rendering/           # PDF rendering
│   │   │   │   │   └── MigraDoc.RtfRendering/        # RTF rendering
│   │   │   │   ├── tests/         # Unit tests
│   │   │   │   └── features/      # Feature tests
│   │   │   └── shared/            # Shared code across platforms
│   │   └── nuget/                 # NuGet package projects
│   └── samples/                   # Sample applications
│       ├── PDFsharp/
│       └── MigraDoc/
├── docs/                          # Internal documentation
└── dev/                           # Development scripts

```

## Key Capabilities

### PDFsharp Capabilities:

1. **PDF Generation**: Create PDF documents from scratch with complete control
2. **PDF Reading**: Parse and read existing PDF documents
3. **PDF Modification**: Edit and enhance existing PDFs
4. **Graphics Drawing**: Comprehensive 2D drawing API similar to GDI+ or WPF
5. **Font Handling**: Support for TrueType, OpenType, and system fonts
6. **Image Support**: Embed various image formats (PNG, JPEG, etc.)
7. **Security**: Encryption, digital signatures, and permission settings
8. **Interactive Forms**: Create and manipulate PDF forms
9. **Annotations**: Add comments, links, and other annotations
10. **PDF/A Support**: Create archival-quality PDF documents

### MigraDoc Capabilities:

1. **High-Level Document Creation**: Define documents using a structured object model
2. **Automatic Formatting**: Text flow, pagination, and layout handled automatically
3. **Professional Layouts**: Tables, columns, headers/footers, and page formatting
4. **Dynamic Content**: Field codes for dates, page numbers, and calculations
5. **Style Management**: Define and apply consistent styles across documents
6. **Cross-Platform**: Works on Windows, Linux, and macOS
7. **Multiple Renderers**: Output to PDF (via PDFsharp) or RTF

## Platform Support

The repository supports multiple builds for different platforms:

- **Core Build**: Cross-platform support for .NET 6, .NET 8, and .NET Standard 2.0
- **GDI Build**: Windows-specific using GDI+ for rendering
- **WPF Build**: Windows-specific using Windows Presentation Foundation

## Technology Stack

- **Language**: C# 12
- **Frameworks**: .NET 6, .NET 8, .NET Standard 2.0
- **Build System**: MSBuild with central package management
- **Version Control**: Git with GitVersion for semantic versioning
- **CI/CD**: Azure Pipelines
- **Dependencies**: Minimal external dependencies (BigGustave for PNG reading in Core build)

## Use Cases

### PDFsharp Use Cases:
- Generate invoices, reports, and certificates
- Create dynamic PDF documents from data
- Add watermarks or annotations to existing PDFs
- Generate barcodes and QR codes
- Create PDF forms for data collection
- Implement document signing workflows

### MigraDoc Use Cases:
- Generate formatted business documents
- Create reports with complex layouts
- Produce invoices with tables and calculations
- Generate letters and mailings
- Create documentation with consistent styling
- Build document templates for reuse

## Getting Started

### Prerequisites:
- .NET SDK (latest version recommended)
- Git repository with at least one commit (required for GitVersion)
- PowerShell 7 (for asset download scripts)

### Build Instructions:
1. Clone the repository
2. Download required assets: `.\dev\download-assets.ps1`
3. Build the solution: `dotnet build`

### Sample Projects:
The repository includes sample applications demonstrating common use cases:
- HelloWorld samples for both PDFsharp and MigraDoc
- Platform-specific samples (Core, GDI, WPF)
- Located in `src/samples/` directory

## Documentation

- Official documentation: https://docs.pdfsharp.net/
- Repository README: Provides quick start and build instructions
- Sample code: Demonstrates library usage patterns
- Internal docs: Technical information in `docs/` directory

## Community and Support

- **Open Source**: Published under MIT License
- **Commercial Support**: Available from empira Software GmbH
- **Community**: Active community of developers using and contributing to the project

## Summary

The PDFsharp & MigraDoc repository provides two complementary libraries for PDF document creation:

- **PDFsharp** offers low-level control for creating and manipulating PDF documents with precise drawing capabilities
- **MigraDoc** provides high-level document creation with automatic layout and formatting

Together, they form a comprehensive solution for .NET developers who need to generate professional PDF documents, from simple reports to complex, richly formatted documents with tables, images, and interactive elements.
