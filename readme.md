# 🏠 Bangalore House Price Predictor

> An end-to-end ML web application that predicts Bangalore house prices using Linear Regression — with a Python/Flask server, interactive frontend, and Nginx deployment on AWS EC2.

![Project Banner](BHP_website.PNG)

---

## 📌 Overview

This data science project walks through a **step-by-step process** of building a real estate price prediction website from scratch — covering everything from raw data cleaning to cloud deployment on AWS EC2.

---

## ✨ What's Covered

### 🧠 Model Building (Data Science Concepts)
- Data loading and cleaning
- Outlier detection and removal
- Feature engineering
- Dimensionality reduction
- GridSearchCV for hyperparameter tuning
- K-Fold Cross Validation
- Linear Regression with Sklearn

### 🖥️ Backend
- Python Flask HTTP server
- Serves predictions via REST API
- Loads the saved trained model

### 🌐 Frontend
- Built with HTML, CSS & JavaScript
- User inputs: BHK, square footage, location, bathrooms
- Calls Flask API and displays predicted price

### ☁️ Deployment
- Hosted on **AWS EC2** (Ubuntu)
- **Nginx** as reverse proxy
- Production-ready setup

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| **Language** | Python |
| **Data Processing** | NumPy, Pandas |
| **Visualization** | Matplotlib |
| **ML Model** | Scikit-learn (Linear Regression) |
| **Backend Server** | Python Flask |
| **Frontend** | HTML, CSS, JavaScript |
| **IDEs** | Jupyter Notebook, VS Code, PyCharm |
| **Cloud** | AWS EC2 |
| **Web Server** | Nginx |

---

## 📁 Project Structure

```
bangalore-house-price-predictor/
│
├── Client/                              # Frontend (HTML, CSS, JS)
│   └── app.html
│
├── Model/                               # Trained ML model & artifacts
│   └── banglore_home_prices_model.pickle
│
├── Server/                              # Flask backend
│   ├── server.py
│   ├── util.py
│   └── requirements.txt
│
├── nginx.file/                          # Nginx config
│   └── bhp.conf
│
├── Banglore_home_prices.ipynb           # EDA & model training (full)
├── banglore_home_prices_final.ipynb     # Final clean notebook
├── bengaluru_house_prices.csv           # Dataset (from Kaggle)
└── README.md
```

---

## 🚀 Getting Started (Local)

### 1. Clone the Repository

```bash
git clone https://github.com/Musawir456/bangalore-house-price-predictor.git
cd bangalore-house-price-predictor
```

### 2. Install Dependencies

```bash
pip install -r Server/requirements.txt
```

### 3. Start Flask Server

```bash
python Server/server.py
```

### 4. Open the App

Open `Client/app.html` in your browser — and start predicting prices! 🎉

---

## ☁️ AWS EC2 Deployment Guide

### Step 1 — Create EC2 Instance

- Launch an **Ubuntu** EC2 instance from AWS Console
- In the **Security Group**, add an inbound rule to allow **HTTP (port 80)** traffic

### Step 2 — Connect to EC2

```bash
ssh -i "C:\Users\YourName\.ssh\Banglore.pem" ubuntu@<your-ec2-public-dns>
```

### Step 3 — Install & Configure Nginx

```bash
sudo apt-get update
sudo apt-get install nginx
```

Check Nginx status:

```bash
sudo service nginx status
```

Start / Stop / Restart:

```bash
sudo service nginx start
sudo service nginx stop
sudo service nginx restart
```

> ✅ Load your EC2 URL in browser — you should see **"Welcome to nginx"**

### Step 4 — Copy Code to EC2

Use **WinSCP** ([download here](https://winscp.net/eng/download.php)) to connect to your EC2 instance and copy all project files to:

```
/home/ubuntu/BangloreHomePrices/
```

### Step 5 — Configure Nginx Reverse Proxy

Create the config file:

```bash
sudo nano /etc/nginx/sites-available/bhp.conf
```

Paste this content:

```nginx
server {
    listen 80;
    server_name bhp;
    root /home/ubuntu/BangloreHomePrices/client;
    index app.html;
    location /api/ {
        rewrite ^/api(.*) $1 break;
        proxy_pass http://127.0.0.1:5000;
    }
}
```

Create symlink and remove default:

```bash
sudo ln -v -s /etc/nginx/sites-available/bhp.conf /etc/nginx/sites-enabled/
sudo unlink /etc/nginx/sites-enabled/default
sudo service nginx restart
```

### Step 6 — Install Python & Start Flask Server

```bash
sudo apt-get install python3-pip
sudo pip3 install -r /home/ubuntu/BangloreHomePrices/server/requirements.txt
python3 /home/ubuntu/BangloreHomePrices/server/server.py
```

> 🚀 Server is now running on **port 5000**

### Step 7 — Access the Live App

Open your EC2 public URL in the browser:

```
http://<your-ec2-public-dns>/
```

Your app is now **live in production!** 🎉

---

## 📊 Dataset

- **Source:** [Kaggle — Bengaluru House Price Data](https://www.kaggle.com/amitabhajoy/bengaluru-house-price-data)
- **File:** `bengaluru_house_prices.csv`
- **Size:** ~904 KB

---

## 🤝 Contributing

Contributions are welcome! Feel free to open an issue or submit a pull request.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/YourFeature`)
3. Commit your changes (`git commit -m 'Add YourFeature'`)
4. Push to the branch (`git push origin feature/YourFeature`)
5. Open a Pull Request

---

## 📄 License

This project is licensed under the **MIT License**.

```
MIT License
Copyright (c) 2026 Abdul Musawir
```

---

## 👤 Author

**Abdul Musawir**
- GitHub: [@Musawir456](https://github.com/Musawir456)

---

## ⭐ Show Your Support

If this project helped you, please give it a **star** ⭐ on GitHub!

---

<p align="center">Built with ❤️ using Scikit-learn, Flask, and AWS EC2</p>



