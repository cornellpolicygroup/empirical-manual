# STATA Commands for Econometrics

## Basic Operations

### Data Management
- **Load a dataset:**

    ```stata
    use "filename.dta", clear
    ```
- **Save a dataset:**

    ```stata
    save "filename.dta", replace
    ```
- **Browse data:**

    ```stata
    browse
    ```
- **Summarize variables:**

    ```stata
    summarize varname
    ```
- **List specific variables:**

    ```stata
    list varname1 varname2
    ```

### Data Import/Export
- **Import CSV:**

    ```stata
    import delimited "filename.csv", clear
    ```
- **Export to CSV:**

    ```stata
    export delimited "filename.csv"
    ```

## Variable Management

### Create, Drop, and Rename Variables
- **Generate new variable:**

    ```stata
    generate newvar = expression
    ```
- **Replace variable values:**

    ```stata
    replace varname = expression
    ```
- **Drop a variable:**

    ```stata
    drop varname
    ```
- **Rename a variable:**

    ```stata
    rename oldvar newvar
    ```

### Label Variables and Values
- **Label a variable:**

    ```stata
    label variable varname "Label description"
    ```
- **Label values of a variable:**

    ```stata
    label define lblname 1 "Label1" 2 "Label2"
    label values varname lblname
    ```

### Missing Values
- **Count missing values:**

    ```stata
    count if missing(varname)
    ```

## Descriptive Statistics and Data Exploration

### Basic Statistics
- **Mean, standard deviation, etc.:**

    ```stata
    summarize varname, detail
    ```
- **Frequency of categorical variables:**

    ```stata
    tabulate varname
    ```

### Cross-tabulation
- **Two-way table:**

    ```stata
    tabulate var1 var2
    ```
- **Add row and column percentages:**

    ```stata
    tabulate var1 var2, row col
    ```

### Correlation Matrix
- **Pairwise correlations:**

    ```stata
    correlate var1 var2 var3
    ```

## Data Transformations

### Recoding Variables
- **Recode values of a variable:**

    ```stata
    recode varname (oldval1 = newval1) (oldval2 = newval2)
    ```

### Generating Categorical Variables
- **Creating dummies (binary variables):**

    ```stata
    generate newvar = (varname == value)
    ```

### Logarithmic and Other Transformations
- **Log of a variable:**

    ```stata
    generate logvar = log(varname)
    ```

### Time Series and Panel Data
- **Set panel data:**

    ```stata
    xtset panelvar timevar
    ```
- **Set time series:**

    ```stata
    tsset timevar
    ```

## Regressions and Statistical Models

### Basic Regression
- **Linear regression:**

    ```stata
    regress depvar indepvar1 indepvar2
    ```
- **Robust standard errors:**

    ```stata
    regress depvar indepvar1, robust
    ```

### Instrumental Variables (IV) Regression
- **Two-stage least squares (2SLS):**

    ```stata
    ivregress 2sls depvar (endogvar = instrumentvar) indepvars
    ```

### Probit and Logit
- **Probit model:**

    ```stata
    probit depvar indepvars
    ```
- **Logit model:**

    ```stata
    logit depvar indepvars
    ```

### Panel Data Models
- **Random effects model:**

    ```stata
    xtreg depvar indepvars, re
    ```
- **Fixed effects model:**

    ```stata
    xtreg depvar indepvars, fe
    ```

### Time Series Models
- **Autoregressive model (AR):**

    ```stata
    arima depvar, ar(1)
    ```
- **Vector autoregression (VAR):**

    ```stata
    var depvar1 depvar2, lags(1/2)
    ```

## Post-estimation and Diagnostics

### Predictions
- **Generate fitted values:**

    ```stata
    predict yhat
    ```
- **Generate residuals:**

    ```stata
    predict residuals, residuals
    ```

### Model Fit Statistics
- **Display regression statistics:**

    ```stata
    estat ic
    ```

### Heteroskedasticity Tests
- **Breusch-Pagan test:**

    ```stata
    estat hettest
    ```

### Multicollinearity Diagnostics
- **Variance inflation factor (VIF):**

    ```stata
    estat vif
    ```

## Graphs and Visualizations

### Basic Graphs
- **Histogram:**

    ```stata
    histogram varname, normal
    ```
- **Scatter plot:**

    ```stata
    scatter var1 var2
    ```

### Regression Plot
- **Add a line to scatter plot:**

    ```stata
    twoway (scatter y x) (lfit y x)
    ```

### Box Plots
- **Boxplot:**

    ```stata
    graph box varname, over(groupvar)
    ```
