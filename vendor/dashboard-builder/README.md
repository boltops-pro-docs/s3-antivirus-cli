<!-- note marker start -->
NOTE: This repo contains only the documentation for the private BoltsOps repo code.
Original file: https://github.com/boltops-pro/s3-antivirus-cli/blob/master/vendor/dashboard-builder/README.md
The docs are publish so they are available for interested subscribers.
For access to the source code, you can become a BoltOps subscriber.
See: https://learn.boltops.com

<!-- note marker end -->

# Dashboard

[![BoltOps Badge](https://img.boltops.com/boltops/badges/boltops-badge.png)](https://www.boltops.com)

This library provides a `Dashboard::Builder` class and some helpers that makes building CloudWatch Dashboards easy.

## Helper Methods

Name | Description
-- | ---
metric_widget | Generates common metric widget. The most used widget.
single_value_metric | Generates single value widget. Example: A counter with the current number of requests.
text_widget | Generates text widget. Useful for informative messages.

## Usage

demo.rb

```ruby
class Demo
  include Dashboard::Helpers
  DEFAULT_REGION = Dashboard::Helpers::DEFAULT_REGION

  def build
    dashboard = Dashboard::Builder.new
    dashboard.add_row(
      scan_widget("ScannedCount"),
      scan_widget("CleanCount"),
      scan_widget("InfectedCount"),
      scan_widget("OversizedCount"),
    )
    dashboard.add_row(
      scan_widget("BytesScanned"),
      text_widget("**Important**\n\nThis dashboard is generated with by s3-antivirus. Manual changes will be replaced."),
    )
    dashboard_body = JSON.pretty_generate(widgets: dashboard.widgets)
    dashboard_name = "S3Antivirus"

    puts "Updating the #{dashboard_name}"
    cloudwatch.put_dashboard(
      dashboard_name: dashboard_name,
      dashboard_body: dashboard_body, # required
    )
  end

  def scan_widget(metric_name, properties={})
    namespace = "S3Antivirus"
    dimension = "Bucket"
    metrics = @buckets.map do |bucket|
      [ namespace, metric_name, dimension, bucket, { period: 60, label: bucket } ]
    end

    default = {
      metrics: metrics,
      stat: "Sum",
      region: DEFAULT_REGION,
    }
    props = default.merge(properties)
    metric_widget(props)
  end
end
```
## Installation

Add this line to the Gemfile:

    gem "dashboard-builder"

And then execute:

    bundle
