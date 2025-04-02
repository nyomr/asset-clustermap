# Dynamic Risk Balancing

This project focuses on **Dynamic Risk Balancing** for various types of assets using Python. The goal is to evaluate and optimize the distribution of risk across a selection of assets by analyzing correlations and clusters. The project uses several popular Python libraries for financial analysis, visualization, and portfolio optimization.

## Requirements

Before running the project, install the necessary dependencies. You can install them using `pip` by running the following commands:
```bash
pip install pandas
pip install riskfolio-lib
pip install pyfolio
pip install yfinance
pip install seaborn
pip install matplotlib
```

## Description

To get started, make sure to install the required libraries listed in the **Requirements** section. After that, prepare your data by downloading asset data using `yfinance`. You can modify the `assets` list to choose the desired assets (equities, forex, cryptocurrencies, etc.).
```bash
assets = [
    "BTC-USD", "ETH-USD", "XRP-USD", "BNB-USD", "SOL-USD", "DOGE-USD", 
    "ADA-USD", "LINK-USD", "AVAX-USD", "SHIB-USD", "HBAR-USD", "OM-USD",
    "UNI-USD", "PEPE24478-USD", "ONDO-USD", "AAVE-USD", "ENA-USD", "ARB-USD",
    "JUP-USD", "OP-USD", "MKR-USD", "LDO-USD", "WIF-USD", "FARTCOIN-USD",
    "PENGU34466-USD", "MEW30126-USD", "ACT-USD", "PNUT-USD", "MOG-USD", 
    "GOAT-USD", "PONKE-USD"
]
```
You can adjust the start and end dates to any range you prefer for your analysis.
```bash
data = yf.download(assets, start="2025-01-01", end="2025-03-30")
```
The script visualizes how assets cluster together based on their correlation by creating a dendrogram. This dendrogram helps to identify relationships between assets, showing which ones are more similar to each other. You can modify the method used to calculate the correlation by changing the `codependence` parameter.
```bash
rp.plot_clusters(
    returns=returns,
    codependence="spearman",
```
| Method   | Suitable For                                         |
|----------|------------------------------------------------------|
| `spearman` | When you want to find relationships between assets that move in the same direction, not necessarily on how the numbers compare directly. For example, if two assets are generally increasing or decreasing together. |
| `pearson` | When you're looking for a linear relationship between assets. Pearson focuses on how similar the actual numbers are. |
| `tail`    | When you're looking at how assets move during extreme situations. This method helps identify which assets change in the same way during stressful times. |

A correlation matrix is created to analyze the relationships between assets, which is then displayed as a heatmap.
```bash
corr_matrix = returns.corr(method="spearman")
```
The correlation of each asset with a specified reference asset (like Bitcoin) is calculated and displayed. You can modify the reference asset to compare correlations with other assets.
```bash
corr = corr_matrix["BTC-USD"].sort_values(ascending=False)
```

## Usage
1. Clone or download the repository to your local machine, or directly open the notebook in **Google Colab**.
2. Install the required libraries listed in the **Requirements** section.
3. Run the `.ipynb` file in your Jupyter Notebook or Google Colab environment.
