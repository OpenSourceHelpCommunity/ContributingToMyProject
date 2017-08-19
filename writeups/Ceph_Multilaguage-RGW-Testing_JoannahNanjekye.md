
# How To Contribute to Ceph - RGW Testing

## What is Ceph

Ceph is a distributed object, block, and file storage platform. It features an interface for Amazon S3 objects inside of its Rados Gateway (RGW).

This RGW's S3 interface is tested and currently has three test suites in python, java and Golang that run against it. These test suites use Amazon SDKs namely boto for python, Go SDK for golang and the Java SDK for Java. In future there may be a c++ test suite as well.

## Getting Involved In Ceph Generally

Generally Contributing to the Ceph project without a very specific purpose or guidance can have a high
barrier to entry. Usually the people that contribute significantly to Ceph are doing it on behalf of their
company and have significant experience in linux/distributed systems/storage.

If someone wanted to make a contribution and weren't be mentored or employed to do so
they would need to be quite the self starter as well because seriously contributing to
Ceph isn't something you can just do off and on.

My recommendation is that you read carefully through the online documentation, watch videos
on it, and build and run a ceph cluster. Then I suggest picking a sub-component of
Ceph to work on (the OSD, RGW, RBD, etc.) and only focus on the component to work on.

Then email ceph-devel asking for a starter project on that specific
sub-component or take a look at the bugs list and try to solve a bug that's not being
worked on in sub-component to get a good understanding of the code.

The list of open issues in Ceph are here:
http://tracker.ceph.com/projects/devops/issues

Here is the info for mailing lists:
http://ceph.com/irc/

## Getting Involved in RGW Testing

Ceph has many [projects](https://github.com/ceph). I will take you through the projects regarding RGW testing. To get involved, you have to first choose what test suite you want to contribute to and if you are not familiar with the programming language then you can go through some tutorials.

### Prerequisites

Most of the instructions in running these tests are based on the fact that you use linux. It is advisable that you get yourself any linux distro like ubuntu or fedora but I would recommend fedora.

You will also need to have a basic understanding of how to use the [Amazon s3 SDKS](https://aws.amazon.com/tools/). There is enough documentation on these SDKS. Go through the details for an sdk depending on the language of the test suite you choose. You can take a look at the developer guides below:

+ [AWS SDK for Go Developer guide](http://docs.aws.amazon.com/sdk-for-go/v1/developer-guide/aws-sdk-go-dg.pdf)
+ [AWS SDK for Java Developer guide](http://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/aws-sdk-java-dg.pdf)
+ [Boto Documentation](http://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/aws-sdk-java-dg.pdf)

### Running RGW

Important to note is the tests run against RGW therefore you need to have it running somewhere. You can set it up in a Linux machine or virtual machine using these guidelines.

Clone Ceph

You can clone from github with

	git clone git@github.com:ceph/ceph

or, if you are not a github user,

	git clone git://github.com/ceph/ceph

Check out Ceph's submodules

	git submodule update --init --recursive

Install dependencies

	./install-deps.sh

Build the vstart target because that is all we need

	./do_cmake.sh
	cd build
	make vstart 

Run vstart

on master

../src/vstart.sh -n -l --rgw_num 1

on kraken branch

../src/vstart.sh -n -l -r


### Checking out and running the Test Suites

#### Go Test suite

Install Go and set GoPath

Ubuntu

	sudo apt-get install golang 
	export GOPATH=$HOME/go

fedora

	dnf install golang 
	export GOPATH=$HOME/go

Clone the test Repository

	git clone https://github.com/nanjekyejoannah/go_s3tests
	cd go_s3tests

Create Configuration by copying sample

	cp config.toml.sample config.toml

Install Dependencies

	go get -d ./...

Run the tests

	cd s3tests
	go test -v 

#### Java Test suite

Clone the test repository

	git clone https://github.com/nanjekyejoannah/java_s3tests
	cd java_s3tests

Create Configuration by copying sample

	cp config.properties.sample config.properties

Install gradle

Ubuntu

	sudo add-apt-repository ppa:cwchien/gradle
	sudo apt-get update
	sudo apt-get install gradle

Fedora

	dnf install gradle

Build the project

	gradle build

Run the tests

	gradle test


#### Python Test suite

To get started, ensure you have the virtualenv software installed; e.g. on Debian/Ubuntu:

	sudo apt-get install python-virtualenv

	and then run:

	./bootstrap

Create a configuration file with the location of the service and two different credentials, something like this:

	[DEFAULT]
	## this section is just used as default for all the "s3 *"
	## sections, you can place these variables also directly there

	## replace with e.g. "localhost" to run against local software
	host = s3.amazonaws.com

	## uncomment the port to use something other than 80
	# port = 8080

	## say "no" to disable TLS
	is_secure = yes

	[fixtures]
	## all the buckets created will start with this prefix;
	## {random} will be filled with random characters to pad
	## the prefix to 30 characters long, and avoid collisions
	bucket prefix = YOURNAMEHERE-{random}-

	[s3 main]
	## the tests assume two accounts are defined, "main" and "alt".

	## user_id is a 64-character hexstring
	user_id = 0123456789abcdef0123456789abcdef0123456789abcdef0123456789abcdef

	## display name typically looks more like a unix login, "jdoe" etc
	display_name = youruseridhere

	## replace these with your access keys
	access_key = ABCDEFGHIJKLMNOPQRST
	secret_key = abcdefghijklmnopqrstuvwxyzabcdefghijklmn

	## replace with key id obtained when secret is created, or delete if KMS not tested
	kms_keyid = 01234567-89ab-cdef-0123-456789abcdef

	[s3 alt]
	## another user account, used for ACL-related tests
	user_id = 56789abcdef0123456789abcdef0123456789abcdef0123456789abcdef01234
	display_name = john.doe
	## the "alt" user needs to have email set, too
	email = john.doe@example.com
	access_key = NOPQRSTUVWXYZABCDEFG
	secret_key = nopqrstuvwxyzabcdefghijklmnabcdefghijklm

Run the tests

	S3TEST_CONF=your.conf ./virtualenv/bin/nosetests

### Contribute! Contribute! Contribute!

You can contribute in many ways by opening an issue or working on the open issues on the projects. A good way to find issues is looking at what tests have not yet been implemented and quickly open an issue.

To find something to work on, look through the to do section of the readme files of the test suites and reach out to the community IRC channel for guidance. You can also choose to work on existing open issues.

Patches can be sent through by opening a pull request on the repositories.

## Ping the community using these platforms

+ On IRC use #ceph-devel - Connect your client to: irc.oftc.net
+ Please send a mail to ceph-community@ceph.com if you would like an invite to the [Ceph slack channel](https://ceph-storage.slack.com/)
+ You can also use the mailing list ceph-devel@vger.kernel.org 

## Happy Hacking!

Ceph is a warm community. You may face some back and forth especially building and running ceph but remember that it always works as @amaredia says. Feel free to reachout to me (@Captain_Joannah on twitter)if you are stuck. I could also help out on especially the java and Go test suites. 

## Useful Links

+ https://github.com/ceph
+ http://ceph.com/irc/
+ https://github.com/ceph/s3-tests
+ https://github.com/nanjekyejoannah/java_s3tests
+ https://github.com/nanjekyejoannah/go_s3tests