# Dataflow Pipeline steps

| Step              | Purpose                |
| ----------------- | ---------------------- |
| Imports           | Load Beam libraries    |
| PipelineOptions   | Configure Dataflow job |
| DoFn Classes      | Business logic         |
| Pipeline Creation | Create Beam pipeline   |
| Read              | Read data from source  |
| Transform         | Apply business rules   |
| Write             | Store processed data   |
| Run               | Execute pipeline       |

```python
# ============================================================
# APACHE BEAM / DATAFLOW - MOST COMMON IMPORTS
# ============================================================

# Core Beam Library
import apache_beam as beam

from apache_beam.options.pipeline_options import PipelineOptions
from apache_beam.options.pipeline_options import StandardOptions
from apache_beam.options.pipeline_options import SetupOptions

from apache_beam.io.gcp.pubsub import ReadFromPubSub
from apache_beam.io.gcp.bigquery import WriteToBigQuery

from apache_beam.transforms.window import FixedWindows

from apache_beam.metrics import Metrics

import json
import logging

# File IO
from apache_beam.io import ReadFromText
from apache_beam.io import WriteToText

# Windowing
from apache_beam.transforms.window import FixedWindows
from apache_beam.transforms.window import SlidingWindows
from apache_beam.transforms.window import Sessions

# Triggers
from apache_beam.transforms.trigger import AfterWatermark
from apache_beam.transforms.trigger import AfterProcessingTime
from apache_beam.transforms.trigger import Repeatedly

# Common Python Libraries
import datetime
import re
import os
import sys
import uuid

# ============================================================
# MOST COMMON TRANSFORMS
# ============================================================
beam.Create()
beam.Map()
beam.FlatMap()
beam.Filter()
beam.ParDo()
beam.GroupByKey()
beam.CombinePerKey()
beam.CoGroupByKey()
beam.Partition()
beam.Flatten()
beam.Distinct()

```
