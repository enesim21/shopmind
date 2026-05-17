# ShopMind - Find Cheaper Fashion Alternatives

Find similar clothes for cheaper prices! ShopMind helps you discover budget-friendly alternatives to luxury brands.

## 🚀 Features

- **3 Search Modes**: Search by text, upload photos, or paste product links
- **Multi-Source Search**: Compare prices across Zara, H&M, Decathlon, Vinted, Leboncoin & more
- **Smart History**: Track all your searches with one click access
- **Save Favorites**: Build your wishlist of great deals
- **Advanced Filters**: Filter by price, brand, color, and size
- **Dashboard**: Track your savings and search statistics
- **Price Alerts**: Get notified when prices drop
- **Dark Luxury UI**: Beautiful, modern dark theme interface

## 🛠️ Tech Stack

- **Frontend**: React 18 + TypeScript
- **Styling**: Tailwind CSS + Framer Motion
- **Backend**: Supabase (Auth + Database)
- **Search API**: SerpAPI (Google Shopping + Web Search)
- **Build**: Vite

## 📋 Setup Instructions

### 1. Clone the Repository
\`\`\`bash
git clone https://github.com/enesim21/shopmind.git
cd shopmind
\`\`\`

### 2. Install Dependencies
\`\`\`bash
npm install
\`\`\`

### 3. Setup Supabase
1. Go to [supabase.com](https://supabase.com) and create a new project
2. Get your API keys from Settings → API
3. Create these tables in Supabase SQL Editor:

\`\`\`sql
-- Users table (auto-created by Supabase Auth)

-- Searches table
CREATE TABLE searches (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  search_query TEXT NOT NULL,
  search_type TEXT NOT NULL,
  results JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Favorites table
CREATE TABLE favorites (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  product_id TEXT NOT NULL,
  product_data JSONB,
  created_at TIMESTAMP DEFAULT NOW()
);

-- Price Alerts table
CREATE TABLE price_alerts (
  id UUID DEFAULT gen_random_uuid() PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES auth.users(id) ON DELETE CASCADE,
  product_name TEXT NOT NULL,
  target_price DECIMAL(10, 2),
  current_price DECIMAL(10, 2),
  source TEXT,
  notified BOOLEAN DEFAULT FALSE,
  created_at TIMESTAMP DEFAULT NOW()
);
\`\`\`

### 4. Setup SerpAPI
1. Go to [serpapi.com](https://serpapi.com) and create a free account
2. Get your API key (100 free requests/month)

### 5. Create `.env.local`
\`\`\`
VITE_SUPABASE_URL=your_supabase_url
VITE_SUPABASE_ANON_KEY=your_supabase_key
VITE_SERPAPI_KEY=your_serpapi_key
\`\`\`

### 6. Run Locally
\`\`\`bash
npm run dev
\`\`\`

Visit [http://localhost:3000](http://localhost:3000)

## 🚀 Build & Deploy

### Build for Production
\`\`\`bash
npm run build
\`\`\`

### Preview Build
\`\`\`bash
npm run preview
\`\`\`

## 📝 API Integration

### Search Products
\`\`\`typescript
import { searchProducts, searchVinted, searchLeboncoin } from './lib/searchAPI'

// Search all sources
const results = await searchProducts('Nike shoes')

// Search specific sources
const vintedResults = await searchVinted('Nike shoes')
const leboncoinResults = await searchLeboncoin('Nike shoes')
\`\`\`

## 📊 Database Schema

### Users
- id (UUID)
- email (string)
- username (string)
- avatar_url (string)

### Searches
- id (UUID)
- user_id (UUID)
- search_query (string)
- search_type (text/image/link)
- results (JSON)
- created_at (timestamp)

### Favorites
- id (UUID)
- user_id (UUID)
- product_id (string)
- product_data (JSON)
- created_at (timestamp)

### Price Alerts
- id (UUID)
- user_id (UUID)
- product_name (string)
- target_price (number)
- current_price (number)
- source (string)
- notified (boolean)
- created_at (timestamp)

## 🎯 Roadmap

- [ ] Image recognition for photo search
- [ ] Email notifications system
- [ ] Affiliate links integration
- [ ] Social sharing features
- [ ] Mobile app
- [ ] AI recommendations
- [ ] Price drop alerts
- [ ] Browser extension

## 💡 How It Works

1. **User searches** for a product (text, photo, or link)
2. **AI processes** the search query
3. **SerpAPI searches** across multiple sources
4. **Results are aggregated** and sorted by price
5. **User can filter** by brand, price, color, size
6. **Favorites are saved** to user's account
7. **Price alerts** notify when deals appear

## 📧 Support

For issues or feature requests, please open an issue on GitHub.

## 📄 License

MIT License - feel free to use this project for your own purposes.

---

**Made with ❤️ by ShopMind Team**
