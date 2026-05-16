# GCP Organization Folder & Project Creation Commands

**Organization ID:** `692154983500` (simplelinks.co)

---

## Step 1: Re-authenticate (if needed)

```bash
gcloud auth revoke sultan@simplelinks.co --quiet
gcloud auth login
```

---

## Step 2: Create top-level folders under organization

```bash
for name in simplelinks-common simplelinks-dev simplelinks-staging simplelinks-prod; do
  gcloud resource-manager folders create --organization=692154983500 --display-name="$name"
done
```

---

## Step 3: Verify top-level folders

```bash
gcloud resource-manager folders list --organization=692154983500
```

Expected output:

| DISPLAY_NAME       | ID             |
|--------------------|----------------|
| simplelinks-common | 312408226729   |
| simplelinks-dev    | 904413161207   |
| simplelinks-staging| 690593726409   |
| simplelinks-prod   | 736551489809   |

---

## Step 4: Create subfolders under each parent folder

### Under simplelinks-common (ID: 312408226729)

```bash
for sub in networking security shared-tools; do
  gcloud resource-manager folders create --folder=312408226729 --display-name="$sub"
done
```

### Under simplelinks-dev (ID: 904413161207)

```bash
for sub in platform data-science apis; do
  gcloud resource-manager folders create --folder=904413161207 --display-name="$sub"
done
```

### Under simplelinks-prod (ID: 736551489809)

```bash
for sub in platform data-science apis; do
  gcloud resource-manager folders create --folder=736551489809 --display-name="$sub"
done
```

---

## Step 5: List subfolders under a parent

```bash
gcloud resource-manager folders list --folder=312408226729   # simplelinks-common
gcloud resource-manager folders list --folder=904413161207   # simplelinks-dev
gcloud resource-manager folders list --folder=736551489809   # simplelinks-prod
```

Expected output:

| Subfolder     | Parent                     | ID             |
|---------------|----------------------------|----------------|
| networking    | folders/312408226729       | 387691659772   |
| security      | folders/312408226729       | 523342655257   |
| shared-tools  | folders/312408226729       | 554286502818   |
| platform      | folders/904413161207       | 689138167871   |
| data-science  | folders/904413161207       | 352432239085   |
| apis          | folders/904413161207       | 115554179107   |
| platform      | folders/736551489809       | 118775576391   |
| data-science  | folders/736551489809       | 570807357591   |
| apis          | folders/736551489809       | 442599456544   |

---

## Step 6: Create projects under subfolders

```bash
gcloud projects create simplelinks-shared-networking   --folder=387691659772 --name="simplelinks-shared-networking"
gcloud projects create simplelinks-dev-platform-gke     --folder=689138167871 --name="simplelinks-dev-platform-gke"
gcloud projects create simplelinks-dev-ds-pipelines     --folder=352432239085 --name="simplelinks-dev-ds-pipelines"
gcloud projects create simplelinks-security-logging     --folder=523342655257 --name="simplelinks-security-logging"
```

---

## Step 7: Verify projects

```bash
gcloud projects list --filter="parent.id:387691659772 OR parent.id:689138167871 OR parent.id:352432239085 OR parent.id:523342655257"
```

---

## Step 8: Full resulting hierarchy

```
simplelinks-common/          (312408226729)
├── networking/              (387691659772)
│   └── simplelinks-shared-networking
├── security/                (523342655257)
│   └── simplelinks-security-logging
└── shared-tools/            (554286502818)

simplelinks-dev/             (904413161207)
├── platform/                (689138167871)
│   └── simplelinks-dev-platform-gke
├── data-science/            (352432239085)
│   └── simplelinks-dev-ds-pipelines
└── apis/                    (115554179107)

simplelinks-prod/            (736551489809)
├── platform/                (118775576391)
├── data-science/            (570807357591)
└── apis/                    (442599456544)

simplelinks-staging/         (690593726409)
```
