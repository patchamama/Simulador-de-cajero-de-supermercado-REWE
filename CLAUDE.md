# CLAUDE.md - AI Assistant Guide for REWE Cashier Simulator

## Project Overview

This is a **REWE Supermarket Cashier Training Simulator** project designed to help cashiers learn product codes, visual product identification, and cash register operations at REWE supermarkets in Germany.

**Project Status:** Documentation phase - No interactive simulator code implemented yet.

**Primary Languages:** Spanish (ES), German (DE), English (EN)

**Target Users:** REWE cashier trainees who need to memorize:
- Product codes (REWE IDs)
- Product names in German
- Visual identification of products (especially bakery items)
- Cash register operation procedures

## Repository Structure

```
.
├── README.md                # Comprehensive documentation (product tables, cashier instructions)
├── productos.json           # Product database (39 products, multilingual)
├── dashboard/               # REWE dashboard screenshots (18 images)
│   ├── dashboard.brötchen._*.jpg  # Bakery section
│   ├── dashboard.gemüse._*.jpg    # Vegetables section
│   ├── dashboard.obst._*.jpg      # Fruits section
│   ├── dashboard.snacks._*.jpg    # Snacks section
│   └── dashboard.süsses._*.jpg    # Sweets section
└── products_pictures/       # Product images for visual training (17 images)
    ├── dashboard.brötchen.*.jpg
    ├── dashboard.gemüse.*.jpg
    ├── dashboard.obst.*.jpg
    └── dashboard.snacks.*.jpg
```

## Data Structure

### productos.json Schema

Each product entry contains:
```json
{
  "es": "Spanish name",
  "de": "German name",
  "en": "English name",
  "rewe_id": 123,           // Product code to memorize
  "unidad": "kg|unidad",    // Unit type
  "categoria": {
    "es": "Category in Spanish",
    "en": "Category in English",
    "de": "Category in German"
  },
  "imagen": "URL to product image",
  "link": "REWE product search URL",
  "comments": {
    "es": "",
    "en": "",
    "de": ""
  }
}
```

### Product Categories

Based on productos.json and dashboard images:
- **Brötchen** (Bakery) - No codes in JSON yet, visual learning only
- **Gemüse** (Vegetables) - Multiple products with codes
- **Obst** (Fruits) - Multiple products with codes
- **Snacks** - Present in dashboard, not in JSON
- **Süsses** (Sweets) - Present in dashboard, not in JSON
- **Sonstiges** (Miscellaneous) - Present in dashboard

## Key Product Information

### Most Important Products to Memorize

From README.md, these are the most frequently sold items:

| REWE ID | Product (DE) | Product (ES) | Unit |
|---------|-------------|--------------|------|
| 100 | REWE Beste Wahl Banane | Plátano Rewe | kg |
| 111 | Gurke | Pepino | unidad |
| 117 | Avocado | Aguacate | unidad |
| 260 | Zucchini | Calabacín | kg |
| 289 | Paprika rot | Pimiento rojo | kg |
| 290 | Paprika gelb | Pimiento amarillo | kg |
| 601 | Chiquita Banane | Plátano chiquita | kg |
| 660 | Rispentomaten | Tomate racimo | kg |
| 721 | Zwiebeln | Cebolla | kg |

### Special Notes

- **BIO products** have codes printed/attached on the wrapper
- **Kakis** have all their codes visible
- **Kiwis** normally have codes
- **DHL unlock code** for scanning device: 3537
- **Bell peppers** (Paprika) must be weighed separately by color
- Price format: No comma - format is euros+cents (e.g., 20€ = 2000, 5.12€ = 512)

## Cashier Operation Instructions

### Money Input Format
- No comma/decimal separator
- Format: EUROCENTIMOS (euros + cents as 4 digits)
- Examples: 20.00€ → 2000, 5.12€ → 512, 0.30€ → 030

### Key Operations

1. **Cash Withdrawal (Auszahlung)**
   - Max: 200€
   - Only with Girokonto/Girocard/EC Card + PIN
   - Enter amount (BETRAG) + "KARTENZAHLUNG"
   - Amount not shown on screen for privacy
   - Always press "KARTENZAHLUNG" after, NOT "SUMME"

2. **Receipt Copies (BONKOPIE)**
   - Can reprint last 3 receipts
   - Select "BONKOPIE" → navigate with repeated presses → "EINGABE" to print

3. **Gift Vouchers (GUTSCHEIN)**
   - Enter amount + EINGABE
   - Confirm or correct amount
   - EINGABE to confirm

4. **Deposits (EINZAHLUNGEN)**
   - Customer scans QR code (mobile/paper)
   - Pay amount in cash (BAR)

5. **Multiple Same Items**
   - Enter quantity + "MENGE" + scan product

6. **Cancellations (Stornos)**
   - "SOFORT STORNO": Cancel last entry
   - "ZEILEN STORNO": Cancel specific line
   - Note: First entry cannot be cancelled until more items added

7. **Price Check**
   - Use "PREIS ABFRAGE" button

8. **Error Recovery**
   - Use "LÖSCHEN" button for any errors, uncertainties, or strange messages

## Development Goals

The README.md identifies these pending features to implement:

### 1. Product Viewer
Create a visual interface to browse productos.json with:
- Display product images
- Show REWE IDs prominently
- Filter by category
- Search functionality
- Multilingual display toggle

### 2. Product Code Learning Quiz
Interactive quiz system to memorize REWE IDs:
- Show product image/name
- Ask for REWE ID
- Validate answer
- Track learning progress
- Focus on most common products

### 3. Visual Product Identification Quiz
Using images from `products_pictures/`:
- Show product image
- Ask for German name
- Multiple choice or text input
- Categories: Brötchen, Obst, Gemüse, Snacks, Süsses
- Spaced repetition learning

### 4. Cashier Operations Quiz
Test knowledge of procedures:
- Scenario-based questions
- Money format conversions
- Operation sequences
- Storno procedures
- Special cases (Gutschein, Auszahlung, etc.)

## Technology Recommendations

Since no code exists yet, consider these approaches:

### Frontend Options
- **HTML/CSS/JavaScript**: Simple, no build step, easy deployment
- **React/Vue**: If building more complex interactive features
- **Python Flask/FastAPI**: For backend + simple web interface

### Features to Implement
1. Product database viewer (read from productos.json)
2. Flashcard system for REWE IDs
3. Image-based quiz using products_pictures/
4. Progress tracking (localStorage or database)
5. Spaced repetition algorithm
6. Mobile-responsive design (for on-the-go learning)

## Coding Conventions

When implementing the simulator, follow these guidelines:

### Multilingual Support
- Always support ES, DE, EN for all UI text
- Use i18n/localization from the start
- Product data already has all three languages

### Data Handling
- productos.json is the single source of truth
- Never hardcode product data
- Validate JSON schema on load
- Handle missing images gracefully

### Code Style
- Use meaningful variable names in English (code comments in ES/DE/EN)
- Keep functions small and focused
- Comment complex business logic (especially cashier operations)

### File Organization
```
/src
  /components      # UI components
  /data           # JSON data files
  /assets         # Images, styles
  /utils          # Helper functions
  /i18n           # Translations
  /quizzes        # Quiz logic
```

## Testing Priorities

When implementing features:

1. **Product Data Validation**
   - All products have required fields
   - URLs are valid
   - REWE IDs are unique

2. **Quiz Logic**
   - Correct answer validation
   - Score calculation
   - Progress persistence

3. **Cashier Operations**
   - Money format conversion
   - Operation sequences
   - Edge cases (first item storno, etc.)

## Git Workflow

- **Main branch**: Production-ready code
- **Feature branches**: Use descriptive names (e.g., `feature/product-viewer`, `feature/quiz-system`)
- **Commit messages**: Clear, concise, in English
  - Format: `type: description` (e.g., `feat: add product code quiz`, `fix: correct money format validation`)

## Important Notes for AI Assistants

### When Adding Features:
1. **Read productos.json first** before suggesting product-related code
2. **Check dashboard images** to understand REWE's actual UI/UX
3. **Reference README.md** for accurate cashier operation details
4. **Maintain multilingual support** in all new features
5. **Don't hardcode product data** - always read from JSON

### When Modifying Products:
- Update productos.json
- Update README.md tables if needed
- Ensure all three languages (ES/DE/EN) are provided
- Verify REWE URLs are properly encoded
- Check image URLs are accessible

### Common Pitfalls to Avoid:
- Don't confuse "unidad" (unit/piece) with "kg" (weight)
- Bell peppers have different codes by color - treat separately
- Money format has no decimal separator in input
- Some products are learned by image only (Brötchen), others by code
- Dashboard categories don't perfectly match productos.json categories yet

## Open Questions (Documented in README)

These need clarification from REWE employees:
1. Beverage crate button? (Kiste/Flasche)
2. When exactly to use "LÖSCHEN" button
3. How do plastic container food items (sold by kg) work?

## External Resources

- **REWE Product Search**: `https://www.rewe.de/shop/productList?search=<producto>`
- **Product Images**: Hosted on `img.rewe-static.de`
- **Dashboard Screenshots**: In `/dashboard` directory
- **Product Pictures**: In `/products_pictures` directory

## Quick Start for Development

```bash
# Clone repository
git clone <repo-url>
cd Simulador-de-cajero-de-supermercado-REWE

# View product data
cat productos.json | jq '.'

# Create feature branch
git checkout -b feature/your-feature-name

# Start building!
# Recommended: Start with simple product viewer
# Then add quiz functionality
# Finally add cashier operation simulator
```

## Contact & Support

If you need clarification on REWE-specific operations or product codes, consult the README.md or ask the repository maintainer who has actual REWE cashier experience.

---

**Last Updated**: 2025-11-22
**Version**: 1.0
**Maintained by**: AI assistants should update this file when making structural changes to the repository
