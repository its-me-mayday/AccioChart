# **AccioChart** 🪄

*"A magical repository to showcase how to publish Helm Charts using GitHub!"*

AccioChart automates Helm Chart packaging, versioning, and publishing via GitHub Actions and GitHub Pages, making it easy to create and manage your own Helm repository.

---

## **Features**
- 📦 **Package Helm Charts**: Automatically package your charts into `.tgz` files.
- 🌐 **Host with GitHub Pages**: Publish your charts on a public Helm repository.
- 🤖 **Automate with GitHub Actions**: Streamline chart updates and releases.

---

## **Repository Structure**

```plaintext
AccioChart/
├── .github/
│   └── workflows/
│       └── release-chart.yml  # GitHub Action for publishing charts
├── charts/
│   └── my-chart/
│       ├── Chart.yaml         # Chart metadata
│       ├── values.yaml        # Default chart values
│       ├── templates/         # Kubernetes manifest templates
│       └── README.md          # Chart-specific instructions
├── .gitignore                 # Ignore unnecessary files
└── README.md                  # This file!
```

---

## **How It Works**

### 1. **Create or Update a Chart**
Place your Helm Chart in the `charts/` directory and ensure the `Chart.yaml` file is properly configured with name, version, and metadata.

### 2. **Commit and Push**
Push changes to the `main` branch to trigger the GitHub Action. The pipeline will:
- Package the chart into a `.tgz` file.
- Update the `index.yaml` file.
- Publish the Helm repository on GitHub Pages.

Example commands:
```bash
$ git add .
$ git commit -m "Update Helm Chart"
$ git push origin main
```

### 3. **Access Your Chart**
After the GitHub Action completes, your Helm repository will be available at:

```
https://<username>.github.io/<repository>/
```

Add the Helm repository to your local environment:
```bash
$ helm repo add acciochart https://<username>.github.io/<repository>
$ helm repo update
```
You can now install your chart with the following command:

```bash
$ helm install my-release acciochart/my-chart
```
This will allow you to deploy your Helm chart to your Kubernetes cluster easily.

## GitHub Action Workflow
The automation is defined in .github/workflows/release-chart.yml. It performs the following steps:

* Installs Helm.
* Packages the chart located in the charts/ directory.
* Updates the Helm repository index.
* Publishes the package and index to GitHub Pages using the gh-pages branch.