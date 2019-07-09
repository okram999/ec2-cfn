ENV=test
STACK_NAME=pm-av-openText-$(ENV)
PROFILE=default
GLOBAL_STACK_NAME=pm-av-openText-$(ENV)
REGION=us-east-1

upload-env:
	#@aws s3api create-bucket --bucket pm-av-opentext-templates-us-east-1-$(ENV) --region us-east-1 
	#@aws s3api put-bucket-tagging --bucket pm-av-opentext-templates-us-east-1-$(ENV) --tagging 'TagSet=[{Key=App,Value=AV-2.0},{Key=BusinessTower,Value=PM},{Key=Department,Value=DT},{Key=BillingApprover,Value=Steve.Yi@cbre.com},{Key=FMC,Value=411407}]'
	@aws s3 cp _main.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/_main.yml
	@aws s3 cp resources/otcs-adm.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/otcs-adm.yml
	@aws s3 cp resources/otcs-ags.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/otcs-ags.yml
	@aws s3 cp resources/otcs-fen.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/otcs-fen.yml
	@aws s3 cp resources/otcs-otac.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/otcs-otac.yml
	@aws s3 cp resources/otcs-otds.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/otcs-otds.yml
	@aws s3 cp resources/rds-otac.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/rds-otac.yml
	@aws s3 cp resources/rds-otag-otcs.yml s3://pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/$(ENV)/rds-otag-otcs.yml
	
create-env:
	@aws cloudformation create-stack \
		--region $(REGION) \
		--stack-name $(STACK_NAME) \
		--template-url https://s3.amazonaws.com/pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/_main.yml \
		--parameters file://parameters.$(ENV).json \
		--capabilities CAPABILITY_IAM \
		--profile $(PROFILE) \
		--tags file://tags.$(ENV).json \
		--disable-rollback

update-env:
	@aws cloudformation update-stack \
		--region $(REGION) \
		--stack-name $(STACK_NAME) \
		--template-url https://s3.amazonaws.com/pm-av-opentext-templates-us-east-1-$(ENV)/cloudformation/_main.yml \
		--parameters file://parameters.$(ENV).json \
		--capabilities CAPABILITY_IAM \
		--profile $(PROFILE) \
		--tags file://tags.$(ENV).json
