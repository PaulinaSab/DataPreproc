# DataPreproc

# Užduotis 3:
Transformuokite duomenų failą donate.sas7bdat į tvarkingą duomenų failą, tam suskurkite
naują kintamąjį donate_rate

## Nuskaitomas duomenų failas

```{r}
library(sas7bdat)
setwd(getwd())
donations = read.sas7bdat("donate.sas7bdat")
```
## Sutvarkome lentelė pagal tidy standartus įtraukiant naują kintamąjį donate rate
```{r}
library(tidyr)
library(tidyverse)
donations = donations %>% pivot_longer(c("Qtr1", "Qtr2", "Qtr3", "Qtr4",), names_to = "quarter", values_to = "donate_rate")
```

## NaN reikšmės pakeičiamos reikšmių vidurkiu
```{r}
donations$donate_rate = ifelse(is.nan(donations$donate_rate), as.integer(mean(donations$donate_rate, na.rm = T)), donations$donate_rate)
```
