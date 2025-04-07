
Limit Order Book – High-Performance Matching Engine

This project is a low-latency Limit Order Book (LOB) and Matching Engine built from scratch in C++, capable of processing over 1.4 million transactions per second (TPS). It supports all standard order types used in modern electronic trading systems, and is designed for high-frequency trading (HFT) and quantitative finance applications.

---

🚀 Features

- Ultra-Fast Matching Engine
  Handles over 1.4 million TPS with average latency of just 713 nanoseconds per order.

- Full Support for Order Types
  - Market Orders
  - Limit Orders (Add, Modify, Cancel)
  - Market Limit Orders
  - Stop Orders (Add, Modify, Cancel)
  - Stop Limit Orders (Add, Modify, Cancel)

- Efficient Data Structures
  AVL trees for managing price levels and doubly-linked lists for order queues, ensuring O(1) operations for key functions.

- Performance Analytics
  In-depth testing framework with latency breakdowns, AVL rebalance tracking, and visualizations using Python.

- Thorough Testing Suite
  Unit and integration tests using GoogleTest to validate all matching engine operations.

---

📁 Project Structure

Limit_Order_Book/
├── Limit_Order_Book/        # Core Matching Engine
│   ├── Book.cpp/hpp
│   ├── Limit.cpp/hpp
│   ├── Order.cpp/hpp
├── Generate_Orders/         # Order generation logic
│   ├── GenerateOrders.cpp/hpp
│   ├── initialOrders.txt
├── Process_Orders/          # Order processing and analysis
│   ├── OrderPipeline.cpp/hpp
│   ├── data_visualisation.py
│   ├── order_processing_times.csv
├── test/                    # Unit and integration tests
│   ├── ExampleOrdersTests.cpp
│   ├── LimitOrderBookTests.cpp
├── figures/                 # Latency graphs and analysis visuals
├── main.cpp                 # Entry point
├── CMakeLists.txt           # Build configuration

---

📊 Architecture Overview

The Limit Order Book uses a combination of AVL Trees and Doubly Linked Lists:

- Limit Tree (AVL) – Maintains sorted price levels for Buy/Sell orders.
- Order Queue (Linked List) – Each price level holds a queue of orders for FIFO execution.
- Stop Order Trees – Separate AVL trees for Stop and Stop Limit orders.

Key objects:

Order {
    int idNumber;
    bool buyOrSell;
    int shares;
    int limit;
    Order *nextOrder;
    Order *prevOrder;
    Limit *parentLimit;
}

Limit {
    int limitPrice;
    int size;
    int totalVolume;
    Limit *parent, *leftChild, *rightChild;
    Order *headOrder, *tailOrder;
}

Book {
    Limit *buyTree, *sellTree;
    Limit *stopBuyTree, *stopSellTree;
    Limit *highestBuy, *lowestSell;
    Limit *highestStopSell, *lowestStopBuy;
}

---

🧪 Testing & Performance

- 5 Million Orders tested with performance analysis
- Latency measured per request using timestamps before and after matching
- Average Latency: ~713 ns/order
- Cancel Order: Fastest (~400 ns), Modify/Stop Orders: Slightly longer
- AVL Rebalances: Significantly increase latency (~2,500 ns per rebalance)
- Data Generator: Produces synthetic realistic market data for stress testing

✅ Achieved throughput of 1.4 million orders per second on Intel i5-12450H @ 2.00GHz.

---

📈 Visual Insights

Performance analytics includes:

- Latency Histogram
- Latency by Order Type
- Latency vs Number of Executed Trades
- Impact of AVL Tree Rebalances
- 3D Latency vs Trades vs Rebalances

All visualizations are available in the figures/ directory and generated via data_visualisation.py.

---

🧠 Insights & Conclusion

- AVL tree balancing is the main contributor to increased latency.
- Optimizations around tree updates and data structures can further increase throughput.
- Upgrading CPU hardware can improve processing capacity beyond 1.4M TPS.

---

📜 License

This project is licensed under the MIT License.

---

🙌 Acknowledgments

- Inspired by:
  - "How to Build a Fast Limit Order Book" – wkselph
  - "Millions of Orders per Second Matching Engine Testing" – Alex Zus

---

📌 Topics

C++ · HFT · Matching Engine · Low Latency · AVL Tree · Quantitative Trading · Order Book · GoogleTest · Market Simulator · Finance
