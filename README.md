Setup Instructions
1. Clone the Repository
git clone https://github.com/your-username/sales-analytics-api.git
cd sales-analytics-api

2. Install Dependencies
npm install

3. Setup Environment Variables
Create a .env file and add your MongoDB connection string:
MONGO_URI=mongodb://localhost:27017/salesDB
PORT=4000

4. Start the Server
node app.js

The API will run at http://localhost:4000/graphql.
GraphQL Queries
1. Get Customer Spending
query {
  getCustomerSpending(customerId: "63f8b3d5a7b1d7f3b0a2c5e1") {
    totalSpent
    averageOrderValue
    lastOrderDate
  }
}

2. Get Top Selling Products
query {
  getTopSellingProducts(limit: 5) {
    productId
    name
    totalSold
  }
}

3. Get Sales Analytics
query {
  getSalesAnalytics(startDate: "2024-01-01", endDate: "2024-12-31") {
    totalRevenue
    completedOrders
    categoryBreakdown {
      category
      revenue
    }
  }
}

Database Models
Customers
const CustomerSchema = new mongoose.Schema({
  name: String,
  email: String,
  age: Number,
  location: String,
  gender: String,
});

Products
const ProductSchema = new mongoose.Schema({
  name: String,
  category: String,
  price: Number,
  stock: Number,
});

Orders
const OrderSchema = new mongoose.Schema({
  customerId: mongoose.Schema.Types.ObjectId,
  products: String, // Stringified JSON Array
  totalAmount: Number,
  orderDate: Date,
  status: String,
});

curl --request POST \
  --header 'content-type: application/json' \
  --url http://localhost:4000/graphql \
  --data '{"query":"query { getSalesAnalytics(startDate: "2024-01-01", endDate: "2025-02-28") {
    totalRevenue
    completedOrders
    categoryBreakdown {
      category
      revenue
    }
  }}"}'
