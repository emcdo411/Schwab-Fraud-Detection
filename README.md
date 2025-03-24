# Schwab Fraud Detection

## 📌 Overview
Schwab Fraud Detection is a **privacy-first fraud detection dashboard** built using **Shiny, XGBoost, and real-time analytics**. This project simulates a **fraud detection system** designed for Charles Schwab, utilizing **machine learning models** to flag high-risk transactions based on authentication patterns and transaction anomalies.

## 🚀 Features
- **Real-time fraud detection** using **XGBoost**.
- **Privacy-first approach**—no personally identifiable information (PII) is stored.
- **Dynamic fraud visualization** with **Shiny & ggplot2**.
- **Authentication trends analysis** for OAuth and **2FA validation insights**.
- **Scalable framework** adaptable to real-world banking fraud scenarios.

## 🛠️ Technologies Used
- **R (Shiny, ggplot2, dplyr, xgboost, httr)**
- **Machine Learning (XGBoost)**
- **Real-time Data Visualization**
- **Fraud Detection & Risk Analytics**

## 🔥 Why This Matters  
In today’s digital world, financial fraud is evolving faster than ever. With **$9.8M lost per breach** (IBM, 2024) and **AI-driven fraud schemes** on the rise, financial institutions like **Charles Schwab** must stay ahead with cutting-edge security measures. This project demonstrates how **machine learning and real-time analytics** can detect anomalies before they become costly breaches.  

By prioritizing **privacy-first fraud detection**, Schwab can **reinforce client trust, reduce financial risk, and uphold its reputation as a leader in wealth management security**. The future of fraud prevention isn’t just about reacting—it’s about proactively **outsmarting fraudsters** before they strike.  

## 🌟 Conclusion  
**Schwab Fraud Detection** is a powerful demonstration of how AI can **enhance security without compromising privacy**. By leveraging **Shiny, XGBoost, and real-time visualizations**, this project provides a scalable and effective fraud detection framework.  

With **continuous improvements**, Schwab and other financial institutions can **adapt, evolve, and stay ahead** in the fight against financial fraud. 🚀  

---

## 📚 Code Implementation
```r
library(shiny)
library(ggplot2)
library(dplyr)
library(xgboost)
library(httr)

# Mock synthetic data (Schwab Westlake clients)
set.seed(2025)
data <- data.frame(
  ClientID = 1:1000,  # Anonymized
  Transaction_Amt = c(rlnorm(900, 10, 2), rlnorm(100, 15, 3)),  # Normal + outliers
  Region = sample(c("Highland Park", "Westlake", "Dallas"), 1000, replace = TRUE),
  OAuth_Valid = sample(c(TRUE, FALSE), 1000, replace = TRUE, prob = c(0.95, 0.05)),
  TwoFA_Passed = sample(c(TRUE, FALSE), 1000, replace = TRUE, prob = c(0.98, 0.02)),
  Fraud_Label = c(rep(0, 900), rep(1, 100))  # 10% fraud
) %>% select(-ClientID)  # Drop PII

# One-hot encode Region (numeric for XGBoost)
encoded_data <- model.matrix(~ . - Fraud_Label, data = data)[, -1]  # Drop intercept
train_matrix <- xgb.DMatrix(data = encoded_data, label = data$Fraud_Label)

# Simple XGBoost model for fraud
model <- xgboost(data = train_matrix, nrounds = 10, objective = "binary:logistic", verbose = 0)
data$Fraud_Prob <- predict(model, train_matrix)

# Shiny UI
ui <- fluidPage(
  titlePanel("SchwabSafe Fraud Shield: Privacy-First Detection"),
  sidebarLayout(
    sidebarPanel(
      selectInput("region", "Region:", choices = unique(data$Region)),
      p("Privacy Stat: 1 breach = $9.8M loss (IBM 2024)")
    ),
    mainPanel(
      plotOutput("fraud_dist"),
      plotOutput("auth_trends")
    )
  )
)

# Shiny Server
server <- function(input, output) {
  filtered_data <- reactive({
    data %>% filter(Region == input$region)
  })
  
  output$fraud_dist <- renderPlot({
    ggplot(filtered_data(), aes(x = Transaction_Amt, fill = Fraud_Prob > 0.5)) +
      geom_histogram(binwidth = 10000, position = "dodge") +
      labs(title = "Transaction Fraud Probability", x = "Amount ($)", fill = "Fraud Risk") +
      scale_fill_manual(values = c("#2ECC71", "#E74C3C")) +
      theme_minimal()
  })
  
  output$auth_trends <- renderPlot({
    ggplot(filtered_data(), aes(x = OAuth_Valid, fill = TwoFA_Passed)) +
      geom_bar(position = "fill") +
      labs(title = "OAuth & 2FA Authentication Trends", y = "Proportion", fill = "2FA Passed") +
      scale_fill_manual(values = c("#FF5733", "#3498DB")) +
      theme_minimal()
  })
}

# Run it
shinyApp(ui, server)
```

---

## 📂 Repository Structure
```
├── app.R  # Main Shiny App File
├── README.md  # Project Documentation
├── data/  # Folder for Sample or Mock Data
└── outputs/  # Folder for Generated Plots and Reports
```

## 🏆 Future Enhancements
- Integrate **real-time Schwab transaction data (simulated API feeds)**.
- Implement **advanced AI/ML models for anomaly detection**.
- Develop a **risk scoring system** for transaction flagging.
- Expand **dashboard capabilities with client-side interaction**.

## 📝 License
This project is for educational and portfolio purposes only and is **not affiliated with Charles Schwab**. 

---

**👨‍💻 Built by [Maurice McDonald]** | 🌐 [# Schwab Fraud Detection

## 📌 Overview
Schwab Fraud Detection is a **privacy-first fraud detection dashboard** built using **Shiny, XGBoost, and real-time analytics**. This project simulates a **fraud detection system** designed for Charles Schwab, utilizing **machine learning models** to flag high-risk transactions based on authentication patterns and transaction anomalies.

## 🚀 Features
- **Real-time fraud detection** using **XGBoost**.
- **Privacy-first approach**—no personally identifiable information (PII) is stored.
- **Dynamic fraud visualization** with **Shiny & ggplot2**.
- **Authentication trends analysis** for OAuth and **2FA validation insights**.
- **Scalable framework** adaptable to real-world banking fraud scenarios.

## 🛠️ Technologies Used
- **R (Shiny, ggplot2, dplyr, xgboost, httr)**
- **Machine Learning (XGBoost)**
- **Real-time Data Visualization**
- **Fraud Detection & Risk Analytics**

## 🔥 Why This Matters  
In today’s digital world, financial fraud is evolving faster than ever. With **$9.8M lost per breach** (IBM, 2024) and **AI-driven fraud schemes** on the rise, financial institutions like **Charles Schwab** must stay ahead with cutting-edge security measures. This project demonstrates how **machine learning and real-time analytics** can detect anomalies before they become costly breaches.  

By prioritizing **privacy-first fraud detection**, Schwab can **reinforce client trust, reduce financial risk, and uphold its reputation as a leader in wealth management security**. The future of fraud prevention isn’t just about reacting—it’s about proactively **outsmarting fraudsters** before they strike.  

## 🌟 Conclusion  
**Schwab Fraud Detection** is a powerful demonstration of how AI can **enhance security without compromising privacy**. By leveraging **Shiny, XGBoost, and real-time visualizations**, this project provides a scalable and effective fraud detection framework.  

With **continuous improvements**, Schwab and other financial institutions can **adapt, evolve, and stay ahead** in the fight against financial fraud. 🚀  

---

## 📚 Code Implementation
```r
library(shiny)
library(ggplot2)
library(dplyr)
library(xgboost)
library(httr)

# Mock synthetic data (Schwab Westlake clients)
set.seed(2025)
data <- data.frame(
  ClientID = 1:1000,  # Anonymized
  Transaction_Amt = c(rlnorm(900, 10, 2), rlnorm(100, 15, 3)),  # Normal + outliers
  Region = sample(c("Highland Park", "Westlake", "Dallas"), 1000, replace = TRUE),
  OAuth_Valid = sample(c(TRUE, FALSE), 1000, replace = TRUE, prob = c(0.95, 0.05)),
  TwoFA_Passed = sample(c(TRUE, FALSE), 1000, replace = TRUE, prob = c(0.98, 0.02)),
  Fraud_Label = c(rep(0, 900), rep(1, 100))  # 10% fraud
) %>% select(-ClientID)  # Drop PII

# One-hot encode Region (numeric for XGBoost)
encoded_data <- model.matrix(~ . - Fraud_Label, data = data)[, -1]  # Drop intercept
train_matrix <- xgb.DMatrix(data = encoded_data, label = data$Fraud_Label)

# Simple XGBoost model for fraud
model <- xgboost(data = train_matrix, nrounds = 10, objective = "binary:logistic", verbose = 0)
data$Fraud_Prob <- predict(model, train_matrix)

# Shiny UI
ui <- fluidPage(
  titlePanel("SchwabSafe Fraud Shield: Privacy-First Detection"),
  sidebarLayout(
    sidebarPanel(
      selectInput("region", "Region:", choices = unique(data$Region)),
      p("Privacy Stat: 1 breach = $9.8M loss (IBM 2024)")
    ),
    mainPanel(
      plotOutput("fraud_dist"),
      plotOutput("auth_trends")
    )
  )
)

# Shiny Server
server <- function(input, output) {
  filtered_data <- reactive({
    data %>% filter(Region == input$region)
  })
  
  output$fraud_dist <- renderPlot({
    ggplot(filtered_data(), aes(x = Transaction_Amt, fill = Fraud_Prob > 0.5)) +
      geom_histogram(binwidth = 10000, position = "dodge") +
      labs(title = "Transaction Fraud Probability", x = "Amount ($)", fill = "Fraud Risk") +
      scale_fill_manual(values = c("#2ECC71", "#E74C3C")) +
      theme_minimal()
  })
  
  output$auth_trends <- renderPlot({
    ggplot(filtered_data(), aes(x = OAuth_Valid, fill = TwoFA_Passed)) +
      geom_bar(position = "fill") +
      labs(title = "OAuth & 2FA Authentication Trends", y = "Proportion", fill = "2FA Passed") +
      scale_fill_manual(values = c("#FF5733", "#3498DB")) +
      theme_minimal()
  })
}

# Run it
shinyApp(ui, server)
```

---

## 📂 Repository Structure
```
├── app.R  # Main Shiny App File
├── README.md  # Project Documentation
├── data/  # Folder for Sample or Mock Data
└── outputs/  # Folder for Generated Plots and Reports
```

## 🏆 Future Enhancements
- Integrate **real-time Schwab transaction data (simulated API feeds)**.
- Implement **advanced AI/ML models for anomaly detection**.
- Develop a **risk scoring system** for transaction flagging.
- Expand **dashboard capabilities with client-side interaction**.

## 📝 License
This project is for educational and portfolio purposes only and is **not affiliated with Charles Schwab**. 

---

**👨‍💻 Built by [Your Name]** | 🌐 [https://github.com/emcdo411]

<img width="956" alt="Screenshot 2025-03-24 111853" src="https://github.com/user-attachments/assets/8f39e37d-b7dd-4535-a641-17d2b776fecc" />
<img width="959" alt="Screenshot 2025-03-24 111612" src="https://github.com/user-attachments/assets/975bfa04-1a3e-4c24-9af4-0901299c5781" />

