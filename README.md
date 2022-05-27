This is a datman-dashboard-ized version of Jer's lovely [niviz-rater app.](https://github.com/jerdra/niviz-rater)

## Installation
1. [install the dashboard](http://imaging-genetics.camh.ca/datman-dashboard/installation.html) if you haven't already.
2. Clone the datman-niviz blueprint into the dashboard's blueprint folder.
```bash
cd datman-dashboard/dashboard/blueprints
git clone git@github.com:DESm1th/datman-niviz.git niviz_rater
```
3. Build the static files. Note that you must have npm installed. If this
step is successful it will have created the folder
`datman-dashboard/dashboard/static/niviz_rater`.
```bash
cd niviz_rater/static_src
npm install
npm run build
```
4. Provide the full path to the configuration file (see the
  Configuration File section for info on constructing one) in the
  `NIVIZ_RATER_CONF` environment variable.
5. Initialize the databases. You must run this as the user that
the dashboard will use to access the database.
```bash
cd datman-dashboard/dashboard/blueprints/niviz_rater/bin
./init_db.py
```

## Configuration File
For the dashboard to host niviz-rater, a configuration file must be provided
using an environment variable named `NIVIZ_RATER_CONF`. This file
must be yaml format and must contain one entry per pipeline.

Each entry must be formatted like below:
```YAML
STUDY_pipeline:
  base_dir: /some/path/to/niviz-rater/input/data
  qc_spec: /some/path/to/niviz-rater/spec_file.yaml
```

`STUDY_pipeline` is the name to use when accessing the data through
    niviz-rater, and the name that will be used for the database.
  - 'STUDY' must be the name of a datman managed study.
  - 'pipeline' must be a unique name for the pipeline data to be displayed
    by niviz-rater
  - Note that 'STUDY' and 'pipeline' MUST be separated by an underscore.

At a minimum you must specify the `base_dir` and `qc_spec` arguments for
each entry. Any additional options you wish to pass to niviz-rater may be
included.