# WoodPecker T-Shirts: Database Q&A System 👕

A natural language to SQL query application powered by Google Palm LLM that enables users to ask questions about t-shirt inventory in plain English and get accurate answers from a MySQL database.

## 🚀 Features

- **Natural Language Queries**: Ask questions about inventory in plain English
- **LLM-Powered SQL Generation**: Uses Google Palm LLM to convert questions to SQL queries
- **Few-Shot Learning**: Implements semantic similarity-based example selection for improved query accuracy
- **Interactive Web Interface**: Built with Streamlit for easy user interaction
- **Inventory Management**: Track t-shirt stock, prices, and discounts across multiple brands
- **Revenue Analysis**: Calculate revenue with and without discounts

## 🏗️ Architecture

The application follows a modern LLM-powered architecture:

1. **Frontend**: Streamlit web interface for user interaction
2. **LLM Integration**: Google Palm for natural language understanding
3. **SQL Generation**: LangChain with custom prompts and few-shot examples
4. **Vector Store**: Chroma DB for semantic similarity matching
5. **Database**: MySQL for t-shirt inventory data

## 📁 Project Structure

```
├── main.py                    # Streamlit web application entry point
├── langchain_helper.py        # Core LLM and database chain logic
├── few_shots.py              # Few-shot learning examples for better query generation
├── requirements.txt          # Python dependencies
├── project_setup.txt         # Setup instructions
├── t_shirt_sales_llm.ipynb   # Jupyter notebook with development process
├── Database/
│   └── db_creation.sql       # MySQL database schema and data
├── result*.png               # Application screenshots and results
└── Terminal_results.png      # Terminal output examples
```

## 🛠️ Installation & Setup

### Prerequisites

- Python 3.8+
- MySQL Server
- Google API Key (Google Palm)

### Step 1: Database Setup

1. Install MySQL and start the service
2. Create the database using the provided SQL script:
   ```bash
   mysql -u root -p < Database/db_creation.sql
   ```

### Step 2: Python Environment

1. Clone the repository and navigate to the project directory
2. Install required dependencies:
   ```bash
   pip install -r requirements.txt
   ```

### Step 3: API Configuration

1. Get a Google API key from [Google AI Studio](https://aistudio.google.com/app/apikey)
2. Create a `.env` file in the project root:
   ```
   GOOGLE_API_KEY=your_google_api_key_here
   ```

### Step 4: Database Configuration

Update the database credentials in `langchain_helper.py` if needed:
```python
db_user = "root"
db_password = "your_password"
db_host = "localhost"
db_name = "woodpecker_tshirts"
```

### Step 5: Run the Application

```bash
streamlit run main.py
```

The application will be available at `http://localhost:8501`

## 💾 Database Schema

### Tables

#### `t_shirts`
- `t_shirt_id` (INT, Primary Key)
- `brand` (ENUM: 'Van Huesen', 'Levi', 'Nike', 'Adidas')
- `color` (ENUM: 'Red', 'Blue', 'Black', 'White')
- `size` (ENUM: 'XS', 'S', 'M', 'L', 'XL')
- `price` (INT, 10-50 range)
- `stock_quantity` (INT)

#### `discounts`
- `discount_id` (INT, Primary Key)
- `t_shirt_id` (INT, Foreign Key)
- `pct_discount` (DECIMAL, 0-100%)

## 🎯 Usage Examples

Ask questions in natural language such as:

- "How many t-shirts do we have left for Nike in XS size and white color?"
- "How much is the total price of the inventory for all S-size t-shirts?"
- "If we have to sell all the Levi's T-shirts today with discounts applied, how much revenue will our store generate?"
- "How many white color Levi's shirts do I have?"

## 🧠 Technical Implementation

### Few-Shot Learning

The application uses semantic similarity-based few-shot learning to improve query accuracy:

1. **Example Storage**: Pre-defined question-SQL-answer examples in `few_shots.py`
2. **Embeddings**: Uses HuggingFace sentence transformers for text embeddings
3. **Vector Store**: Chroma DB stores embeddings for similarity search
4. **Selection**: Retrieves most similar examples for context

### LLM Chain

The core chain combines:
- Google Palm LLM for natural language understanding
- Custom MySQL prompt templates
- Few-shot examples for context
- SQL database integration via LangChain

## 📊 Key Files Description

### `main.py`
Streamlit web interface that:
- Creates the user input form
- Calls the LangChain helper functions
- Displays query results

### `langchain_helper.py`
Core application logic including:
- Database connection setup
- LLM initialization (Google Palm)
- Few-shot prompt template configuration
- Semantic similarity example selector
- SQL database chain creation

### `few_shots.py`
Contains pre-defined examples for few-shot learning:
- Question-SQL-Answer triplets
- Covers common inventory queries
- Helps improve LLM query generation accuracy

### `Database/db_creation.sql`
Complete database setup including:
- Table creation with proper constraints
- Stored procedure for data population
- Sample discount data insertion

## 🎨 Features Demonstrated

1. **Inventory Queries**: Stock levels by brand, size, color
2. **Revenue Calculations**: With and without discounts
3. **Complex Joins**: T-shirts with discount information
4. **Aggregations**: SUM, COUNT operations
5. **Natural Language Understanding**: Converting English to SQL

## 🔧 Dependencies

- `langchain==0.0.284` - LLM framework
- `streamlit==1.22.0` - Web interface
- `mysql-connector-python` - Database connectivity
- `sentence-transformers` - Text embeddings
- `chromadb` - Vector database
- `python-dotenv` - Environment variables
- `faiss-cpu` - Vector similarity search
- `google-generativeai` - Google Palm integration

## 🚀 Advanced Features

- **Semantic Similarity**: Automatically selects the most relevant examples
- **Error Handling**: Graceful handling of SQL query errors
- **Prompt Engineering**: Custom MySQL-specific prompts
- **Vector Embeddings**: Efficient similarity matching for examples

## 📈 Results

The application successfully demonstrates:
- Accurate natural language to SQL conversion
- Improved query accuracy with few-shot learning
- Real-time inventory analysis capabilities
- User-friendly web interface

Screenshots of results are available in the `result*.png` files showing various query examples and their outputs.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Test thoroughly
5. Submit a pull request

## 📝 Notes

- The database is populated with sample data using a stored procedure
- The application uses Google Palm LLM which requires an API key
- Few-shot examples can be customized for different domains
- The database schema can be adapted for other inventory types

## 🔍 Troubleshooting

- Ensure MySQL service is running
- Verify Google API key is correctly set in `.env`
- Check database credentials in `langchain_helper.py`
- Ensure all dependencies are installed via `requirements.txt`

## 📄 License

This project is for educational and demonstration purposes. Please ensure you comply with Google's API usage terms and any other third-party service requirements.

---

**Built with ❤️ using LangChain, Google Palm LLM, and Streamlit** 