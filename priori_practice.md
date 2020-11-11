# Priori Algorithm practice for association analysis of Text(a.k.a. market basket analysis)
# A package named "arules" is specialized for the association analysis.
install.packages("arules")
library(arules)

# Reading csv named "health" 
health <- read.csv("C:\\Users\\User\\Desktop\\health.csv", header=T)
health
health <- readLines("C:\\Users\\User\\Desktop\\health.csv") # Reading in lines(문자열로 읽어오기)
health

# Data need to be transformed into "tranaction" for association analysis
# Data are splited by ',' for converting the form into "transaction
health_trans <- strsplit(health, ",")

# Coverting form of "transaction" 
health_trans <- as(health_trans, "transactions")
health_trans
inspect(health_trans) # This form can be analyzed by association method.

# Extracting associative rules(support >= 0.1, confidence >= 0.8)
# lhs = condition, rhs = result, support = 지지도, confidence = 신뢰도, 
# lift = 향상도, count = numbers of occurence of associative rules(연관성 규칙이 발생한 건수)
health_apriori <- apriori(health_trans, parameter = list(support=0.1, confidence=0.8))
health_apriori                          
inspect(health_apriori)

# Checking data over 1.2 lift
inspect(subset(health_apriori, subset = lift > 1.2))

# Checking data in condition containing "건강"
inspect(subset(health_apriori, subset = lhs %in% c("건강")))

# Checking data in condition containing "건강" and "식품"
inspect(subset(health_apriori, subset = lhs %ain% c("건강", "식품")))
