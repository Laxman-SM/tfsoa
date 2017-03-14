# Terraform State of Awareness (TFSOA)

A dashboard that helps centralize and monitor disparate [Terraform remote states](https://www.terraform.io/docs/state/).

<img width="992" alt="screen shot 2017-01-08 at 4 39 17 pm" src="https://cloud.githubusercontent.com/assets/538171/21755064/ad03c942-d5c1-11e6-991c-6e226f56b3e0.png">

TFSOA accepts pushes of remote Terraform states in a local database.
The Terraform version, JSON serial, JSON version and entire state are saved. TFSOA uses
this information across a multitude of states to present a single dashboard interface
to view statistics on all Terraform states.


### Setup database

```
bundle exec rake db:environment:set
bundle exec rake db:setup
bundle exec rake db:migrate
```

### Start TFSOA

```bash
rackup
```
This will start a rack server on port 9292

### Add your first Terraform state to tfsoa, using your AWS Role you created

```bash
curl 127.0.0.1:9292/tfsoa/add_tf_state \
  -H "Content-Type: application/json" \
  -X \
  POST -d '{"role_arn": "arn:aws:iam::357170183134:role/s3read","s3_bucket_name": "terraform-autozane-remote-state","s3_bucket_key": "golang-app-dev/promotion/Terraform"}'
```

### Development Notes

Current entity-relationship diagram

<img width="1158" alt="screen shot 2017-01-02 at 6 37 01 pm" src="https://cloud.githubusercontent.com/assets/538171/21599015/e581df58-d11a-11e6-817f-3ea81895bd98.png">

### Thank you

Thanks to [Smashing gem](https://github.com/Smashing/smashing) for providing a solid framework for tfsoa to utilize
