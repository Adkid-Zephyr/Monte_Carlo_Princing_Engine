# Monte_Carlo_Princing_Engine
a Monte-Carlo pricing engine for equity-linked snowball autocallables — 20 k antithetic paths, daily knock-in/out checks—delivering PV and Delta with plug-and-play barrier/volatility surfaces

# Snowball Extend Project

Project Introduction
This is a Python program for calculating the quote coupon of a Snowball structured product
It uses Monte Carlo simulation to generate paths of the underlying asset prices calculates the present value PV of the product and adjusts the coupon to make the PV close to 0 to determine the quote coupon of the Snowball product

Project Structure
snowball_extend.py the main program file containing product parameter settings single path valuation function Greeks calculation function and main program logic

Function Description
Product Parameters
The program contains a series of product parameters such as the initial underlying price annual volatility risk - free rate dividend rate knock - out observation days knock - out prices knock - in barrier etc These parameters can be adjusted according to actual needs

Monte Carlo Simulation
It generates multiple paths of the underlying asset prices through Monte Carlo simulation Each path is generated based on a stochastic volatility model considering factors such as the initial underlying price volatility risk - free rate etc

Path Valuation
For each path the product value under that path is calculated according to knock - in knock - out events and product terms and then discounted The path valuation function calculates the corresponding payoffs based on different scenarios knock - out not knocked - in and not knocked - out knocked - in and not knocked - out

Quote Coupon Calculation
By adjusting the coupon the average of the discounted values PV of all paths is made close to 0 The coupon at this time is the quote coupon of the Snowball product

Usage
Ensure that Python and the dependency library numpy are installed
Save the code as snowball_extend.py
Modify the product parameters in the code such as the initial underlying price volatility risk - free rate etc to suit actual needs
Run the program
python snowball_extend.py
The program will output the adjusted quote coupon and the time used

Example Output
PV notional = 0.000
Quote Coupon = 12.345
Time used = 12.34 s

Notes
This program is for educational and research purposes only In actual applications it should be adjusted according to specific product terms and market conditions
The number of Monte Carlo simulation paths N_PATHS and random seed SEED can be modified as needed
The program uses a simplified discount factor calculation method 365 - day annualized which can be adjusted to a trading day basis if needed

Author
FENGSHUO LIU

Copyright
This project follows the MIT License LICENSE



# CHINESE Readme
# Snowball Extend 项目

## 项目简介
这是一个用于计算雪球结构产品（Snowball）报价票息的 Python 程序。它通过蒙特卡洛（Monte Carlo）模拟生成标的资产价格路径，计算产品的贴现价值（PV），并通过调整票息使 PV 接近于 0，从而确定雪球产品的报价票息。

## 项目结构
- `snowball_extend.py`：主程序文件，包含产品参数设置、单条路径估值函数、希腊值计算函数以及主程序逻辑。

## 功能说明
### 1. 产品参数
程序中包含一系列产品参数，如期初标的价格、年化波动率、无风险利率、股息率、敲出观察日、敲出价格、敲入障碍等。这些参数可以根据实际需求进行调整。

### 2. 蒙特卡洛模拟
通过蒙特卡洛模拟生成多条标的资产价格路径。每条路径的生成基于随机波动模型，考虑了标的资产的初始价格、波动率、无风险利率等因素。

### 3. 路径估值
对于每条路径，根据敲入、敲出事件以及产品条款计算该路径下的产品价值，并进行贴现处理。路径估值函数会根据不同的情景（敲出、未敲入且未敲出、敲入且未敲出）计算相应的收益。

### 4. 报价票息计算
通过调整票息，使所有路径的贴现价值（PV）的平均值接近于 0。此时的票息即为雪球产品的报价票息。

## 使用方法
1. 确保已安装 Python 以及依赖库（`numpy`）。
2. 将代码保存为 `snowball_extend.py` 文件。
3. 修改代码中的产品参数（如标的初始价格、波动率、无风险利率等）以适应实际需求。
4. 运行程序：
   ```bash
   python snowball_extend.py
   ```
5. 程序将输出调整后的报价票息以及计算所用时间。

## 示例输出（在我提供的代码中）
PV(% notional) = 1.121 %
Delta          = 0.2145
Gamma          = -0.161385
Time used      = 3.93 s


## 注意事项
- 本程序仅用于学习和研究目的，实际应用中需根据具体产品条款和市场情况进行调整。
- 蒙特卡洛模拟的路径数（`N_PATHS`）和随机种子（`SEED`）可根据需要进行修改。
- 程序中使用了简化的贴现因子计算方式（365 天年化），如有需要可调整为交易日基准。

## 作者
FENGSHUO LIU

## 版权声明
本项目遵循 [MIT License](LICENSE)。
