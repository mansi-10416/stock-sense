importt as st

st.set_page_config(
    page_title="Stock Sense",
    page_icon="📈",
    layout="centered"
)

st.title("📈 STOCK SENSE")
st.write("Stock Market Prediction App")

stock = st.text_input("Enter Stock Symbol (e.g. AAPL)")

if st.button("Get Started"):
    st.success(f"Welcome! You entered: {stock}")
    
import streamlit as st

st.set_page_config(
    page_title="Stock Sense",
    page_icon="📈",
    layout="centered"
)

st.image("assets/logo.png", width=180)

st.markdown("<h1 style='text-align: center;'>Stock Sense</h1>", unsafe_allow_html=True)
st.markdown("<p style='text-align: center;'>AI Powered Stock Market Prediction App</p>", unsafe_allow_html=True)

st.divider()

stock = st.text_input("Enter Stock Symbol (e.g. AAPL, TCS, INFY)")
days = st.slider("Prediction Days", 1, 30, 7)

if st.button("Predict Stock Price"):
    st.success(f"Prediction started for {stock} for next {days} days 📊")
import streamlit as st
import pandas as pd
import yfinance as yf
import plotly.express as px

st.title("Stock Market App")

# Download stock data
ticker = "AAPL"
data = yf.download(ticker, period="1mo", interval="1d")

# Reset index so 'Date' becomes a column
data = data.reset_index()

# Flatten MultiIndex columns
if isinstance(data.columns, pd.MultiIndex):
    # Take the second level if first is empty, else first level
    data.columns = [col[1] if col[0]=='' else col[0] for col in data.columns]

# Check columns
st.write("Columns:", data.columns)
st.write(data.head())

# Create Plotly chart
fig = px.line(data, x="Date", y="Close", title=f"{ticker} Closing Prices")

# Display in Streamlit
st.plotly_chart(fig)
