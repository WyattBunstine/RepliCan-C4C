<img src=".assets/replican.png" width="100%">

# RepliCan: Reproducibility Challenge

Thank you for your interest in contributing to our materials science paper reproducibility benchmark! Please follow these guidelines to submit paper reproduction instructions.

## How to Contribute

### Step 1: Fill out the Online Form 

1. Visit our [submission form: https://JHU-CLSP.github.io/RepliCan-C4C/](https://JHU-CLSP.github.io/RepliCan-C4C/)
2. Fill out all required fields
3. Generate and download your submission file

### Step 2: Submit to Our Repository

#### Option 1: Fork and Make a PR
1. Fork this repository to your personal GitHub account and add files to `submissions/`
2. Make a Pull Request

#### Option 2: Upload File
1. Send us an email with your GitHub username, and we'll grant you write permissions.
2. Navigate to the `submissions/` directory, select **Add file**, then **Upload files**
3. Select **Create a new branch for this commit and start a pull request** with your contribution


### Step 3: Quality Control

We will follow up with you if we have questions or need clarification through GitHub PR discussions and provide peer review information through email.

## Data Schema

### Required Fields

Every submission must include these fields:

- `username`: Your GitHub username
- `paper_title`: Full title of the paper
- `paper_pdf`: URL to the paper PDF (e.g., arXiv, journal website)
- `identifier`: Paper identifier (e.g., arXiv ID, DOI)
- `code_url`: URL to the code repository (GitHub or other)
- `claims`: List of reproducible claims with instructions (at least one required)
- `non_reproducible_claims`: List of non-reproducible claims with reasons

### Optional Fields

- `data_url`: URL to datasets (if separate from code)

### Claims Structure

Each claim must have:
- `claim`: The specific claim from the paper you're documenting
- `instruction`: A list of step-by-step instructions to reproduce the claim (array of strings)

## File Format

### Supported Formats

- JSON (`.json`)
- YAML (`.yaml`)


## Examples

See example files in the `submissions/` directory:
- [`example_submission_in.json`](submissions/example_submission_in.json)
- [`we_also_accept_submission_in.yaml`](submissions/we_also_accept_submission_in.yaml)

## Example YAML Structure

```yaml
username: "materials_researcher"
paper_title: "High-throughput discovery of novel hybrid metal-organic frameworks for carbon capture"
paper_pdf: "https://arxiv.org/pdf/2301.12345.pdf"
identifier: "10.1038/s41563-023-01234-5"
claim_type: "custom_code"
code_url: "https://github.com/materials-discovery/mof-screening"
data_url: "https://materialsproject.org/materials/mp-12345"

claims:
  - claim: "DFT calculations show a bandgap of 3.2 eV for the synthesized perovskite structure."
    instruction:
      - "cd dft_calculations"
      - "python setup_vasp.py --structure ../structures/perovskite.cif"
      - "sbatch run_bandgap.sh"
      - "python parse_eigenval.py EIGENVAL"
      - "Bandgap should report 3.2 ± 0.1 eV"

  - claim: "The ionic conductivity reaches 8.4 mS/cm at 300K for the Li10GeP2S12 structure."
    instruction:
      - "python md_simulation.py --structure Li10GeP2S12.cif --temperature 300 --steps 100000"
      - "python calculate_msd.py trajectory.xyz --species Li"
      - "python nernst_einstein.py msd.dat --temperature 300"
      - "Conductivity value should be 8.4 ± 0.2 mS/cm"

non_reproducible_claims:
  - claim: "The synthesized material shows 95% capacity retention after 1000 charge-discharge cycles."
    reason: "Requires physical battery assembly and electrochemical testing equipment that cannot be computationally reproduced"
    
```

## Validation

Your submission will be automatically validated when you create a Pull Request. The validation checks:

1. File format (must be valid JSON or YAML)
2. All required fields are present and non-empty
3. URLs are properly formatted
4. At least one claim with instructions is provided
5. Username format is valid
6. Code repository URL is provided

## What Happens After Merge

Once your PR is merged:
1. Your submission file will be automatically moved to `data/organized/<your-username>/`
2. The original file in `submissions/` will be removed
3. Multiple submissions from the same user will be grouped together

## Tips for Good Reproduction Instructions

- Be specific about software versions and dependencies
- Include exact commands that can be copy-pasted into a terminal
- Specify expected outputs and acceptable ranges
- Note computational requirements (time, memory, GPUs)
- Include checksums or commit hashes for reproducibility

## Questions?

If you have questions about the data structure or submission process, feel free to open an issue in this repository.