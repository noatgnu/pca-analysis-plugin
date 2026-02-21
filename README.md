# PCA Analysis

**ID**: `pca-analysis`  
**Version**: 1.0.0  
**Category**: analysis  
**Author**: CauldronGO Team

## Description

Principal Component Analysis for dimensionality reduction and visualization

## Runtime

- **Environments**: `python`

- **Script**: `pca.py`

## Inputs

| Name | Label | Type | Required | Default | Visibility |
|------|-------|------|----------|---------|------------|
| `input_file` | Input File | file | Yes | - | Always visible |
| `annotation_file` | Sample Annotation File | file | No | - | Always visible |
| `columns_name` | Sample Columns | column-selector (multiple) | Yes | - | Always visible |
| `n_components` | Number of Components | number (min: 2, max: 10, step: 1) | Yes | 2 | Always visible |
| `log2` | Apply Log2 Transform | boolean | No | false | Always visible |

### Input Details

#### Input File (`input_file`)

Data matrix file containing samples and measurements


#### Sample Annotation File (`annotation_file`)

Optional annotation file for sample grouping and coloring (Sample, Condition, Batch, Color)


#### Sample Columns (`columns_name`)

Select columns containing sample data for PCA analysis

- **Column Source**: `input_file`

#### Number of Components (`n_components`)

Number of principal components to compute


#### Apply Log2 Transform (`log2`)

Apply log2 transformation to the data before PCA


## Outputs

| Name | File | Type | Format | Description |
|------|------|------|--------|-------------|
| `pca_output` | `pca_output.txt` | data | tsv | PCA coordinates for each sample |
| `explained_variance` | `explained_variance_ratio.json` | data | json | Variance explained by each principal component |

## Sample Annotation

This plugin supports sample annotation:

- **Samples From**: `columns_name`
- **Annotation File**: `annotation_file`

## Visualizations

This plugin generates 1 plot(s):

### PCA Scatter Plot (`pca-scatter`)

- **Type**: scatter
- **Component**: `PcaPlot`
- **Data Source**: `pca_output`
- **Customization Options**: 9 available

## Requirements

- **Python Version**: >=3.11

### Package Dependencies (Inline)

Packages are defined inline in the plugin configuration:

- `numpy>=1.24.0`
- `pandas>=2.0.0`
- `scikit-learn>=1.3.0`

> **Note**: When you create a custom environment for this plugin, these dependencies will be automatically installed.

## Example Data

This plugin includes example data for testing:

```yaml
  columns_name: [C:\Raja\DIA-NN searches\June 2022\LT-CBQCA-Test_DIA\RN-DS_220106_BCA_LT-IP_01.raw C:\Raja\DIA-NN searches\June 2022\LT-CBQCA-Test_DIA\RN-DS_220106_BCA_LT-IP_02.raw C:\Raja\DIA-NN searches\June 2022\LT-CBQCA-Test_DIA\RN-DS_220106_BCA_LT-IP_03.raw C:\Raja\DIA-NN searches\June 2022\LT-CBQCA-Test_DIA\RN-DS_220106_BCA_LT-MockIP_01.raw C:\Raja\DIA-NN searches\June 2022\LT-CBQCA-Test_DIA\RN-DS_220106_BCA_LT-MockIP_02.raw C:\Raja\DIA-NN searches\June 2022\LT-CBQCA-Test_DIA\RN-DS_220106_BCA_LT-MockIP_03.raw]
  n_components: 2
  log2: true
  input_file: diann/imputed.data.txt
  columns_name_source: diann/imputed.data.txt
```

Load example data by clicking the **Load Example** button in the UI.

## Usage

### Via UI

1. Navigate to **analysis** → **PCA Analysis**
2. Fill in the required inputs
3. Click **Run Analysis**

### Via Plugin System

```typescript
const jobId = await pluginService.executePlugin('pca-analysis', {
  // Add parameters here
});
```
