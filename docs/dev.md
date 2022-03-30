---
layout: default
title: Tool Developer 
nav_order: 11
description: "Just the Docs is a responsive Jekyll theme with built-in search that is easily customizable and hosted on GitHub Pages."
has_children: true
---

# For analysis tool developer

```GRAB``` package provides a generic framework of GWAS on a large-scale biobank data. The below gives details about how to incorporate a new tool.

Suppose that the method is "ABCDE", then the following functions are required.
- checkControl.NullModel.ABCDE(control, optionGRM)
- fitNullModel.ABCDE(response, designMat, subjData, control, optionGRM, genoType, markerInfo)
- checkControl.Marker.ABCDE(control, optionGRM)
- checkControl.Region.ABCDE(control, optionGRM)
- 

## Function ```checkControl.NullModel.ABCDE```

### Input
- control: a list of parameters  
- optionGRM:

### Output
- control: a list

## Function ```fitNullModel.ABCDE```

### Input
- response:
- designMat: 
- subjData
- control
- optionGRM
- genoType
- markerInfo

### Output
- control: a list

## Function ```checkControl.Marker.ABCDE```

## Function ```checkControl.Region.ABCDE```


