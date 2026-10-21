# CFFMSSP-QI Benchmark Dataset

Benchmark instances for the Complex Fuzzy Flexible Manufacturing System Scheduling Problem with Quality Inspection (CFFMSSP-QI).

## Overview

This repository provides 30 Excel-format scheduling instances associated with a three-stage manufacturing setting: **processing → quality inspection → assembly**. The assembly stage includes component assembly and final product assembly, subject to bill-of-materials (BOM) precedence and kitting constraints. Processing and assembly times are represented using triangular fuzzy numbers (TFNs); manual quality-inspection times are represented using generalized trapezoidal fuzzy numbers (GTrFNs).

## Instance groups

| Group | IDs in the manuscript | Number of instances | Products per instance |
| --- | --- | ---: | ---: |
| Small | S01–S10 | 10 | 10 |
| Medium | M01–M10 | 10 | 30 |
| Large | L01–L10 | 10 | 50 |

The original Excel filenames identify their groups using the Chinese prefixes `小规模` (small), `中规模` (medium), and `大规模` (large), followed by the two-digit instance number. For example, `论文算例数据_小规模05.xlsx` corresponds to **S05**.

## Excel workbook layout

The following structure was verified in the supplied **S05** workbook. Verify consistency across the remaining files before applying this description to the entire dataset.

| Worksheet (original name) | English interpretation | Columns |
| --- | --- | --- |
| `加工质检` | Processing and quality inspection | `产品` (product), `部件` (component), `工件` (workpiece), `工序ID` (operation ID), `类型` (operation type), `时间配置` (resource–time assignments) |
| `部件装配` | Component assembly | `产品` (product), `部件` (component), `组成工件` (constituent workpieces), `工序ID` (operation ID), `装配配置` (assembly-machine–time assignments) |
| `产品总装` | Final product assembly | `产品` (product), `组成部件` (constituent components), `工序ID` (operation ID), `总装配置` (final-assembly-machine–time assignments) |

### Operation and resource notation

- `P#`: product; `C#`: component; `J#`: workpiece.
- `O(i,j)`: the j-th processing operation associated with workpiece index i.
- `QC(i)`: quality inspection associated with workpiece index i.
- `OC(i,j)`: component-assembly operation; `OP(i,j)`: final-product-assembly operation.
- `M#`: processing machine; `Q#`: inspection workstation; `A#`: assembly machine. In S05, component and final assembly both use the `A` resource set.

The resource–time fields contain semicolon-separated candidate assignments, such as:

```text
M1:(27,29,30);M2:(55,65,74)
Q1:(18,22,34,38);Q2:(15,18,32,39)
A1:(36,38,39);A2:(36,46,88)
```

The three-number tuples denote TFN time parameters. The four-number tuples denote GTrFN time parameters; the membership height used for manual inspection in the associated study is 0.8. The first number in each tuple is the lower support endpoint, and the remaining entries follow in ascending order. The workbook does not itself encode the membership height in the example inspection fields.

### Precedence and BOM relationships

The `加工质检` sheet groups workpiece operations by product and component. The `部件装配` sheet lists the workpieces required for each component, and the `产品总装` sheet lists the components required for each product. These relationships support the assembly kitting constraints discussed in the associated manuscript.

## Reproducibility notes

The files store instance input data, not executable scheduling algorithms or verified optimal schedules. To reproduce results, readers will need to implement the resource assignment, fuzzy-time arithmetic and ranking, operation precedence, inspection, and assembly constraints described in the associated paper and supplementary material.

## Related publication

**Working manuscript title:** *Complex Flexible Fuzzy Scheduling Problem with Quality Inspection: An LLM-SPHHA Incorporating Relative Dominance Ranking*.

Add the final paper citation and DOI once they are available.

## Citation and license

Please cite the associated publication when available. A `CITATION.cff` file can be added once the dataset authors and preferred citation have been confirmed. Usage permissions should be clarified with the dataset contributors before adding a license.
