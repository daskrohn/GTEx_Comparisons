# GTEx_Comparisons
Comparing the functional associations of RBD and PD GWAS loci in GTEx v8.  

## Set up:
```R
require(tidyr)
require(dplyr)
require(ggplot2)

setwd("~/Desktop/Projects/GWAS/MR/QTL/")
data = read.csv("GTEx_browser_results.csv", header = T)
data = subset(data, Tissue == "Brain")
attach(data)
```

## Heatmap:
```R
hm <- ggplot(data = data, mapping = aes(x = Concat,
                                                y = Subtissue,
                                                fill = NES)) + geom_tile(color = "black") +
  theme(axis.text.x = element_text(angle = 60, hjust = 1)) +
  scale_fill_gradient2(low="red", mid="white", high="blue", midpoint=0) +
  geom_text(aes(label = GTEx_Flair))
  
hm = hm + xlab("") + ylab("Brain Tissue") + ggtitle("GTEx v8 Expression") + 
  theme(plot.title = element_text(hjust = 0.5, face = "bold")) +
  labs(fill = "eQTL effect size") 

hm

hm + facet_wrap(~Gene, scales = "free_x")

ggsave("gtex_v8_PDvRBD.png", dpi=300)
```
