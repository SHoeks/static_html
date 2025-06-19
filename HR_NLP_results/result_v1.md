
# model

model tested: DeepSeek R1 Turbo

# prompt

### current prompt (2025_06_19)
```txt
Instructions:
You are an expert in analyzing and extracting data from ecological research papers. Your task is to extract information about home ranges. 
The input text is a full scientific paper in which home ranges are estimated.
The output should be formatted according to the predefined JSON formatting provided below. 
```
```JSON
{
    "Home range": [numeric value]; 
    "Home range unit": [unit the home range is provided in]; 
    "Species": [species for which the home range was estimated]; 
    "Sex": "male" | "female" | "mixed";
    "Number of individuals" [number of individuals included in home range estimate];
    "Home range method" [algorithm used for estimating the home range];
} 
```
```txt
Base your answer only on the input text provided. 

Input text:
[full text extracted from html]
```

### potential improvements
- provide example extraction
- add additional entries to JSON

# results

### study id: 67
[paper link](https://onlinelibrary.wiley.com/doi/full/10.1002/ajp.23119)
```JSON
[
    {
        "Home range": 40.01,
        "Home range unit": "km²",
        "Species": "Pan troglodytes",
        "Sex": "male",
        "Number of individuals": 14,
        "Home range method": "minimum convex polygon (MCP)"
    }
]
```
results are correct, but HomeRange has more extractions: 14 individual level home ranges (these are provided in a table which the model failed to extract).

### study id: 228
[paper link](https://link.springer.com/article/10.1007/s10531-013-0551-z)
```JSON
[
    {
        "Home range": 51.8,
        "Home range unit": "ha",
        "Species": "Plecotus auritus",
        "Sex": "female",
        "Number of individuals": 8,
        "Home range method": "100% Minimum Convex Polygon (MCP)"
    },
    {
        "Home range": 295.5,
        "Home range unit": "ha",
        "Species": "Plecotus austriacus",
        "Sex": "female",
        "Number of individuals": 8,
        "Home range method": "100% Minimum Convex Polygon (MCP)"
    },
    {
        "Home range": 239.5,
        "Home range unit": "ha",
        "Species": "Plecotus macrobullaris",
        "Sex": "female",
        "Number of individuals": 8,
        "Home range method": "100% Minimum Convex Polygon (MCP)"
    }
]
```
results are correct, but HomeRange has more extractions: 8+8+8 individual level home ranges (these are provided in a table which the model failed to extract).

### study id: 812
[paper link](https://academic.oup.com/jmammal/article/94/5/1169/869487)
```JSON
[
    {
        "Home range": 79.3,
        "Home range unit": "ha",
        "Species": "Paradoxurus hermaphroditus",
        "Sex": "male",
        "Number of individuals": 6,
        "Home range method": "95% minimum convex polygon (MCP)"
    },
    {
        "Home range": 29.8,
        "Home range unit": "ha",
        "Species": "Paradoxurus hermaphroditus",
        "Sex": "female",
        "Number of individuals": 6,
        "Home range method": "95% minimum convex polygon (MCP)"
    }
]
```
results are correct, but HomeRange has more extractions: 12 individual level home ranges (these are provided in a table which the model failed to extract).

### study id: 1773
[paper link](https://link.springer.com/article/10.1007/s10329-013-0394-y)
```JSON
[
    {
        "Home range": 93,
        "Home range unit": "ha",
        "Species": "Hoolock leuconedys",
        "Sex": "male",
        "Number of individuals": 3,
        "Home range method": "grid method"
    }
]
```
results are almost correct, but HomeRange has more extractions (for different home range estimation methods, also MCP for example)

### study id: 2053
[paper link](https://www.cambridge.org/core/journals/oryx/article/spatial-organization-and-social-relations-in-a-reintroduced-population-of-endangered-iberian-lynx-lynx-pardinus/F92A6C9400CF4E780F2F64D1FADD1CBF)
```JSON
[
    {
        "Home range": 11.18,
        "Home range unit": "km²",
        "Species": "Lynx pardinus",
        "Sex": "male",
        "Number of individuals": 10,
        "Home range method": "fixed kernel estimator"
    },
    {
        "Home range": 9.87,
        "Home range unit": "km²",
        "Species": "Lynx pardinus",
        "Sex": "female",
        "Number of individuals": 10,
        "Home range method": "fixed kernel estimator"
    }
]
```
results are again correct, but HomeRange has more extractions (for all the underlying individual ranges, here are just the averages).

### study id: 2238
[paper link](https://www.sciencedirect.com/science/article/abs/pii/S1616504717300198)
```JSON
[
    {
        "Home range": 181.4,
        "Home range unit": "km2",
        "Species": "Panthera onca",
        "Sex": "female",
        "Number of individuals": 2,
        "Home range method": "Not specified",
        "Tracking method": "satellite GPS collars"
    },
    {
        "Home range": 431.6,
        "Home range unit": "km2",
        "Species": "Panthera onca",
        "Sex": "male",
        "Number of individuals": 2,
        "Home range method": "Not specified",
        "Tracking method": "satellite GPS collars"
    },
    {
        "Home range": 34.3,
        "Home range unit": "km2",
        "Species": "Puma concolor",
        "Sex": "female",
        "Number of individuals": 1,
        "Home range method": "Not specified",
        "Tracking method": "satellite GPS collars"
    },
    {
        "Home range": 72.0,
        "Home range unit": "km2",
        "Species": "Puma concolor",
        "Sex": "male",
        "Number of individuals": 2,
        "Home range method": "Not specified",
        "Tracking method": "satellite GPS collars"
    }
]
```
- results are correct, but HomeRange has more extractions, for all the underlying individual ranges, here are just the averages, although it did pick up one single individual level value, this is because it was mentioned as a example in the text (extreme low home range value). 
- here I added tracking method, because it was confusing the home range estimation method with the tracking method. I indeed also could't find the home range method, but perhaps this is because the text was not complete (RU as not subscription for the journal or something along these lines).


### study id: 2315
[paper link](https://brill.com/view/journals/ab/62/4/article-p479_9.xml?language=en&srsltid=AfmBOopQZ0KP7fuexjk9b85Sbh4XvGes2mUXtCbdmMpoH9foDco20g1q)
```JSON
[
    {
        "Home range": 5.42,
        "Home range unit": "km2",
        "Species": "Meles meles",
        "Sex": "mixed",
        "Number of individuals": 5,
        "Home range method": "MCP 100%"
    }
]
```
results are correct, but HomeRange has more extractions (for all the underlying individual ranges, here are just the average).


