# R Commands for Econometrics

## Basic Operations

### Data Management

- **Load a dataset (CSV):**

    ```r
    data <- read.csv("filename.csv")
    ```

- **Save a dataset:**

    ```r
    write.csv(data, "filename.csv", row.names = FALSE)
    ```

- **View data:**

    ```r
    View(data)
    ```

- **Summarize variables:**

    ```r
    summary(data$varname)
    ```

- **Display specific variables:**

    ```r
    data[c("varname1", "varname2")]
    ```

### Data Import/Export

- **Import CSV:**

    ```r
    data <- read.csv("filename.csv")
    ```

- **Export to CSV:**

    ```r
    write.csv(data, "filename.csv", row.names = FALSE)
    ```

## Variable Management

### Create, Drop, and Rename Variables

- **Create new variable:**

    ```r
    data$newvar <- expression
    ```

- **Replace variable values:**

    ```r
    data$varname <- ifelse(condition, new_value, data$varname)
    ```

- **Drop a variable:**

    ```r
    data$varname <- NULL
    ```

- **Rename a variable:**

    ```r
    names(data)[names(data) == "oldvar"] <- "newvar"
    ```

### Label Variables and Values

- **Rename factor levels:**

    ```r
    data$varname <- factor(data$varname, levels = c(1, 2), labels = c("Label1", "Label2"))
    ```

### Missing Values

- **Count missing values:**

    ```r
    sum(is.na(data$varname))
    ```

## Descriptive Statistics and Data Exploration

### Basic Statistics

- **Mean, standard deviation, etc.:**

    ```r
    summary(data$varname)
    ```

- **Frequency of categorical variables:**

    ```r
    table(data$varname)
    ```

### Cross-tabulation

- **Two-way table:**

    ```r
    table(data$var1, data$var2)
    ```

- **Add row and column proportions:**

    ```r
    prop.table(table(data$var1, data$var2), margin = 1)  # row proportions
    prop.table(table(data$var1, data$var2), margin = 2)  # column proportions
    ```

### Correlation Matrix

- **Pairwise correlations:**

    ```r
    cor(data[c("var1", "var2", "var3")], use = "complete.obs")
    ```

## Data Transformations

### Recoding Variables

- **Recode values of a variable:**

    ```r
    data$varname <- ifelse(data$varname == oldval, newval, data$varname)
    ```

### Generating Categorical Variables

- **Creating dummies (binary variables):**

    ```r
    data$newvar <- as.numeric(data$varname == value)
    ```

### Logarithmic and Other Transformations

- **Log of a variable:**

    ```r
    data$logvar <- log(data$varname)
    ```

### Time Series and Panel Data

- **Create a time series object:**

    ```r
    ts_data <- ts(data$varname, start = c(year, month), frequency = 12)
    ```

- **Set up panel data (using plm package):**

    ```r
    library(plm)
    pdata <- pdata.frame(data, index = c("id", "time"))
    ```

## Regressions and Statistical Models

### Basic Regression

- **Linear regression:**

    ```r
    model <- lm(depvar ~ indepvar1 + indepvar2, data = data)
    summary(model)
    ```

- **Robust standard errors (using sandwich package):**

    ```r
    library(sandwich)
    library(lmtest)
    coeftest(model, vcov = vcovHC(model, type = "HC1"))
    ```

### Instrumental Variables (IV) Regression

- **Two-stage least squares (using ivreg package):**

    ```r
    library(AER)
    model_iv <- ivreg(depvar ~ endogvar + indepvars | instrumentvar + indepvars, data = data)
    summary(model_iv)
    ```

### Probit and Logit

- **Probit model:**

    ```r
    model_probit <- glm(depvar ~ indepvars, family = binomial(link = "probit"), data = data)
    summary(model_probit)
    ```

- **Logit model:**

    ```r
    model_logit <- glm(depvar ~ indepvars, family = binomial(link = "logit"), data = data)
    summary(model_logit)
    ```

### Panel Data Models

- **Random effects model (using plm package):**

    ```r
    library(plm)
    model_re <- plm(depvar ~ indepvars, data = pdata, model = "random")
    summary(model_re)
    ```

- **Fixed effects model:**

    ```r
    model_fe <- plm(depvar ~ indepvars, data = pdata, model = "within")
    summary(model_fe)
    ```

### Time Series Models

- **Autoregressive model (AR):**

    ```r
    arima(data$varname, order = c(1, 0, 0))
    ```

- **Vector autoregression (VAR) (using vars package):**

    ```r
    library(vars)
    model_var <- VAR(data[c("var1", "var2")], p = 2)
    summary(model_var)
    ```

## Post-estimation and Diagnostics

### Predictions

- **Generate fitted values:**

    ```r
    data$yhat <- predict(model)
    ```

- **Generate residuals:**

    ```r
    data$residuals <- residuals(model)
    ```

### Model Fit Statistics

- **Display model summary (AIC, BIC, etc.):**

    ```r
    AIC(model)
    BIC(model)
    ```

### Heteroskedasticity Tests

- **Breusch-Pagan test (using lmtest package):**

    ```r
    library(lmtest)
    bptest(model)
    ```

### Multicollinearity Diagnostics

- **Variance inflation factor (VIF) (using car package):**

    ```r
    library(car)
    vif(model)
    ```

### Marginal Effects

- **Calculate marginal effects:**

    ```r
    library(margins)
    margins(model)
    ```

- **Summary of marginal effects:**

    ```r
    summary(margins(model))
    ```

- **Marginal effects at specific values:**

    ```r
    margins(model, at = list(varname = c(value1, value2)))
    ```

### Hypothesis Testing

- **F-test for linear restrictions:**

    ```r
    library(car)
    linearHypothesis(model, "var1 = var2")
    ```

- **Test joint significance:**

    ```r
    linearHypothesis(model, c("var1 = 0", "var2 = 0"))
    ```

- **Wald test:**

    ```r
    library(aod)
    wald.test(Sigma = vcov(model), b = coef(model), Terms = c(2, 3))
    ```

### Linear Combinations and Contrasts

- **General linear hypothesis testing:**

    ```r
    library(multcomp)
    glht(model, linfct = "var1 + var2 = 0")
    ```

- **Custom contrasts:**

    ```r
    library(multcomp)
    K <- matrix(c(1, 1, 0), 1)  # var1 + var2
    glht(model, linfct = K)
    ```

### Model Comparison

- **Compare nested models:**

    ```r
    anova(model1, model2)
    ```

- **Likelihood ratio test:**

    ```r
    library(lmtest)
    lrtest(model1, model2)
    ```

## Graphs and Visualizations

### Basic Graphs

- **Histogram:**

    ```r
    hist(data$varname, main = "Histogram", xlab = "Variable")
    ```

- **Scatter plot:**

    ```r
    plot(data$var1, data$var2)
    ```

### Regression Plot

- **Add a regression line to scatter plot:**

    ```r
    plot(data$var1, data$var2)
    abline(model, col = "blue")
    ```

### Box Plots

- **Boxplot:**

    ```r
    boxplot(varname ~ groupvar, data = data)
    ```

## Packages

### Installing Packages

```r
install.packages("packagename")
```

### Loading Packages

```r
library(packagename)
```

### Recommended Packages

- **`stargazer`:** Create publication-quality tables.

    ```r
    install.packages("stargazer")
    library(stargazer)
    ```

- **`texreg`:** Export regression tables in LaTeX, HTML, Word.

    ```r
    install.packages("texreg")
    library(texreg)
    ```

- **`modelsummary`:** Modern table output with many formats.

    ```r
    install.packages("modelsummary")
    library(modelsummary)
    ```

- **`AER`:** Contains `ivreg` for instrumental variables regressions.

    ```r
    install.packages("AER")
    library(AER)
    ```

- **`plm`:** Panel data regressions.

    ```r
    install.packages("plm")
    library(plm)
    ```

- **`fixest`:** Fast fixed effects estimation.

    ```r
    install.packages("fixest")
    library(fixest)
    ```

- **`sandwich`:** Robust standard errors.

    ```r
    install.packages("sandwich")
    library(sandwich)
    ```

- **`car`:** Regression diagnostics and multicollinearity tests.

    ```r
    install.packages("car")
    library(car)
    ```

- **`lmtest`:** Tests for linear models.

    ```r
    install.packages("lmtest")
    library(lmtest)
    ```

- **`vars`:** Vector autoregressive models.

    ```r
    install.packages("vars")
    library(vars)
    ```

- **`margins`:** Calculate and visualize marginal effects.

    ```r
    install.packages("margins")
    library(margins)
    ```

- **`broom`:** Convert models into tidy data frames for easy visualization.

    ```r
    install.packages("broom")
    library(broom)
    ```

- **`multcomp`:** Multiple comparisons and general linear hypotheses.

    ```r
    install.packages("multcomp")
    library(multcomp)
    ```

- **`aod`:** Analysis of overdispersed data and additional model tests.

    ```r
    install.packages("aod")
    library(aod)
    ```

- **`ggplot2`:** Advanced data visualization.

    ```r
    install.packages("ggplot2")
    library(ggplot2)
    ```