# Retail Analytical System (RAS)

A powerful, intelligent inventory and sales management platform designed to transform traditional retail operations into a data-driven decision-support system. Built with Java Swing and MySQL, this system combines real-time inventory tracking with advanced predictive analytics.

![License](https://img.shields.io/badge/license-MIT-blue.svg)
![Java](https://img.shields.io/badge/java-11%2B-orange.svg)
![MySQL](https://img.shields.io/badge/mysql-8.0%2B-blue.svg)

## 🎯 Features

### Core Inventory Management
- **Real-Time Stock Tracking** – Automatic inventory updates after every transaction
- **Purchase & Sales Operations** – Seamless recording of stock inflows and outflows
- **Product Management** – Complete control over product details (ID, name, price, quantities)
- **Low-Stock Alerts** – Visual warnings when inventory falls below reorder levels

### Advanced Analytics & Predictions
- **Predictive Stock Depletion** – Forecast the exact date when stock will run out
- **Revenue Forecasting** – Estimate cumulative sales for future periods
- **Sales Trend Analysis** – Identify patterns and seasonal trends in historical data
- **Future Stock Projections** – Predict remaining inventory after predicted demand events
- **Linear Regression Predictions** – User-friendly forecasting on selected variables

### Data Management & Reporting
- **Dynamic Filtering** – Multi-criteria filters on transactions, dates, and products
- **Comprehensive History** – Complete audit trail of all inventory operations
- **Excel Export** – Generate detailed reports with filtered data and analytics
- **Historical Analytics** – Query and analyze transaction history with ease

### Security & Access Control
- **Role-Based Authentication** – Separate admin and user access levels
- **BCrypt Password Hashing** – Industry-standard security with salt protection
- **Secure Credentials** – Encrypted password storage with no plain-text data
- **Privilege Separation** – Admins have full control; users get restricted access

## 🛠 Technology Stack

| Component | Technology |
|-----------|-----------|
| **Frontend** | Java Swing GUI |
| **Backend** | MySQL 8.0+ |
| **Connectivity** | JDBC |
| **Security** | BCrypt with Salt |
| **Export** | Apache POI (Excel) |
| **Platform** | Windows OS |

## 📋 System Requirements

- **Java**: JDK 11 or higher
- **MySQL**: 8.0 or higher
- **RAM**: Minimum 2GB
- **Disk Space**: 500MB (including database)
- **OS**: Windows 10/11 (or compatible)

## 🚀 Quick Start

### Prerequisites
```bash
# Ensure Java is installed
java -version

# Ensure MySQL is running
mysql --version
```

### Installation

1. **Clone the Repository**
```bash
git clone https://github.com/yourusername/retail-analytical-system.git
cd retail-analytical-system
```

2. **Set Up Database**
```bash
# Connect to MySQL
mysql -u root -p

# Run the database initialization script
source database/init_schema.sql
source database/insert_sample_data.sql
```

3. **Configure Database Connection**
Edit `config/DatabaseConfig.java`:
```java
private static final String URL = "jdbc:mysql://localhost:3306/retail_db";
private static final String USER = "root";
private static final String PASSWORD = "your_password";
```

4. **Compile & Run**
```bash
# Compile all Java files
javac -d bin src/**/*.java

# Run the application
java -cp bin:lib/* com.retail.LoginWindow
```

## 💻 Usage Guide

### For Normal Users
1. **Login** with your username and password
2. **Manage Inventory**:
   - Click `Purchase` to add new products
   - Click `Additional Purchase` to restock items
   - Click `Sale` to record sales transactions
3. **Analyze Data**:
   - Use `Filter` for dynamic queries
   - Use `Predict` for simple linear regression forecasts
   - Use `Export to Excel` for reporting

### For Administrators
All user features plus:
1. **Product Management**:
   - Click `Update` to modify product details
   - Click `Delete` to remove products
2. **Advanced Analytics** (via History):
   - Date when stock will run out
   - Cumulative revenue forecasts
   - Sales trend analysis
   - Future stock projections
3. **Full Report Generation**:
   - Export filtered or complete histories
   - Generate predictive analytics reports

## 🗄 Database Schema

### Tables

#### `inventorymanagementtable` (Master Inventory)
```sql
CREATE TABLE inventorymanagementtable (
    Product_Id INT PRIMARY KEY,
    Product_Name VARCHAR(100) NOT NULL,
    Price DECIMAL(10,2) NOT NULL,
    Quantity INT NOT NULL,
    Total_Purchase INT NOT NULL,
    Total_Sale INT NOT NULL
);
```

#### `producttransactions` (Transaction History)
```sql
CREATE TABLE producttransactions (
    Transaction_Id INT PRIMARY KEY AUTO_INCREMENT,
    Product_Id INT NOT NULL,
    Product_Name VARCHAR(100) NOT NULL,
    Date_Of_Transaction DATETIME NOT NULL,
    Quantity_Changed INT NOT NULL,
    Price DOUBLE NOT NULL,
    Total_Purchase DOUBLE,
    Total_Sale DOUBLE,
    Quantity_After INT NOT NULL,
    Cumulative_Purchase INT,
    Cumulative_Sale INT,
    FOREIGN KEY (Product_Id) REFERENCES inventorymanagementtable(Product_Id)
);
```

## 🔐 Security Features

### Authentication
- **Role-Based Access Control (RBAC)**
  - **Admin Role**: Full access to all features
  - **User Role**: Limited to purchase, sale, filtering, simple predictions, and export

### Password Security
- **BCrypt Hashing**: Each password is hashed with a unique salt
- **No Plain-Text Storage**: Passwords are never stored in readable format
- **Attack Resistance**: Protected against brute-force and rainbow table attacks

### Data Protection
- **Transaction Logging**: Every operation is recorded for audit trails
- **Access Restrictions**: Users can only access their permitted features
- **Data Integrity**: Secure credential management prevents unauthorized modifications

## 📊 Key Algorithms

### Predictive Analytics
- **Linear Regression**: Used for trend analysis and forecasting
- **Cumulative Analysis**: Tracks running totals for revenue and inventory
- **Trend Slope Calculation**: Identifies sales patterns and seasonal variations

### Dynamic Query Generation
- Filters generate SQL queries based on user input
- Supports multi-criteria filtering on date ranges, products, and metrics
- Real-time analytics on selected data subsets

## 📁 Project Structure

```
retail-analytical-system/
├── src/
│   ├── com/retail/
│   │   ├── LoginWindow.java
│   │   ├── UserWindow.java
│   │   ├── AdminWindow.java
│   │   ├── HistoryWindow.java
│   │   ├── DatabaseConnection.java
│   │   ├── PasswordHashing.java
│   │   └── PredictiveAnalytics.java
│   └── ...
├── database/
│   ├── init_schema.sql
│   └── insert_sample_data.sql
├── config/
│   └── DatabaseConfig.java
├── lib/
│   ├── mysql-connector.jar
│   ├── poi-*.jar
│   └── bcrypt.jar
└── README.md
```

## 🧪 Testing

### Sample Credentials
```
Admin Login:
  Username: admin
  Password: admin@123

User Login:
  Username: user
  Password: user@123
```

### Test Scenarios
1. Login with admin and user accounts
2. Create new products via Purchase functionality
3. Record sales transactions
4. Apply filters on inventory data
5. Run predictive analytics
6. Export data to Excel
7. Verify low-stock alerts trigger correctly

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

### Development Guidelines
- Follow Java naming conventions
- Document public methods with JavaDoc
- Add unit tests for new features
- Update README for significant changes

## 📈 Future Enhancements

- [ ] Multi-user concurrent access optimization
- [ ] Cloud database integration (AWS RDS, Azure SQL)
- [ ] REST API for third-party integrations
- [ ] Mobile app companion (Android/iOS)
- [ ] Advanced machine learning models (Prophet, ARIMA)
- [ ] Real-time dashboard with charts and KPIs
- [ ] Supplier management module
- [ ] Customer segmentation analytics

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Dhruv Yadav**
- Enrollment: 105252000342
- Program: M.C.A. (Software Engineering)
- Institution: Guru Gobind Singh Indraprastha University (GGSIPU), New Delhi

**Supervisor**: Dr. Sonam (Assistant Professor), USICT GGSIPU

## 📚 References

- [MySQL Documentation](https://dev.mysql.com/doc/)
- [Java Swing Tutorials](https://docs.oracle.com/javase/tutorial/uiswing/)
- [JDBC Tutorial](https://docs.oracle.com/javase/tutorial/jdbc/)
- [Apache POI Documentation](https://poi.apache.org/)
- [BCrypt Security](https://www.mindrot.org/projects/jBCrypt/)

## 📞 Support

For issues, questions, or suggestions:
1. Check existing [GitHub Issues](../../issues)
2. Create a new issue with detailed description
3. Include screenshots or error logs if applicable
4. Tag with appropriate labels (bug, enhancement, documentation)

## 🙏 Acknowledgments

- GGSIPU for academic guidance and resources
- Apache POI for Excel export functionality
- BCrypt library for secure password hashing
- MySQL community for database management tools

---

**Last Updated**: October 28, 2025  
**Status**: Active Development
