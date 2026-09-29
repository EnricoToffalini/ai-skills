# R style patterns

Use these examples as calibration, not rigid templates.

## Prefer: transparent loop

```r
niter = 1000
results = data.frame(beta=rep(NA,niter), p=NA)

for(i in 1:niter){
  x = rnorm(200)
  y = 0.2*x + rnorm(200)
  fit = lm(y ~ x)
  results$beta[i] = coef(fit)[2]
  results$p[i] = summary(fit)$coef[2,4]
}

mean(results$p < .05)
```

Do not replace this with `map_dfr()`, nested anonymous functions, or a custom simulation framework unless there is a practical gain.

## Prefer: direct data preparation

```r
df = read.csv("data/data.csv")
df = df[!is.na(df$outcome),]
df$group = factor(df$group, levels=c(0,1), labels=c("control","treatment"))
fit = lm(outcome ~ group + age, data=df)
summary(fit)
```

A few explicit steps are preferable to a long pipe.

## Prefer: minimal comments

```r
# main model
fit = lmer(score ~ condition*time + (1|id), data=df)
summary(fit)

# sensitivity analysis without outliers
df2 = df[abs(scale(df$score)) < 3,]
fit2 = lmer(score ~ condition*time + (1|id), data=df2)
```

Do not comment every assignment.

## Prefer: function only where it earns its keep

For a costly simulation that will be parallelized:

```r
simOne = function(N, beta){
  x = rnorm(N)
  y = beta*x + rnorm(N)
  fit = lm(y ~ x)
  summary(fit)$coef[2,4]
}

library(parallel)
cl = makeCluster(6)
clusterExport(cl, c("simOne", "N", "beta"))
p = unlist(parLapply(cl, 1:5000, function(i) simOne(N,beta)))
stopCluster(cl)

mean(p < .05)
```

Here the function is justified by parallel execution.

## Prefer: cheap code can fail normally

```r
df = read.csv("data/data.csv")
fit = lm(y ~ x1 + x2, data=df)
summary(fit)
```

Do not wrap ordinary analysis in input validation plus `tryCatch()` merely to produce friendlier errors.

## Prefer: protect genuinely expensive iterations

```r
simOne = function(i){
  tryCatch({
    dat = simulate_data()
    fit = difficult_model(dat)
    c(beta=coef(fit)["x"], ok=1)
  }, error=function(e) c(beta=NA, ok=0))
}
```

Keep the recovery small. The goal is to avoid losing the whole run, not to build a fault-tolerant application.

## Prefer: ggplot2 directly

```r
library(ggplot2)

ggplot(df, aes(x=age, y=score, color=group))+
  geom_point(alpha=.5)+
  geom_smooth(method="lm", se=FALSE)+
  theme_bw()
```

Do not create a plotting helper unless many plots repeat the same non-trivial structure.

## Prefer: self-contained file

A paper analysis script should usually contain, in order:

```r
library(readxl)
library(lavaan)
library(ggplot2)

set.seed(123)

df = read_excel("data/data.xlsx")

# data preparation
...

# main analysis
...

# figure
...

ggsave("figs/main-figure.png", width=7, height=5, dpi=300)
```

Avoid `source("R/helpers.R")`, `source("R/config.R")`, and several layers of helper files unless the project really needs them.

## Editing rule

If existing code uses a different harmless convention, preserve it. Style consistency is secondary to a small, auditable patch.
