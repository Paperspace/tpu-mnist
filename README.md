# Gradient changes to Google's TPU MNIST tutorial

These source files are taken from the Google tutorial files for running the TPU MNIST tutorial.  The original source files are unchanged, but the way the sample is run in Paperspace Gradient is different than as described in Google's documentation.  This README describes the differences.

Note: the original README file for these sources is [README_ORIG.md](README_ORIG.md)

To run the MNIST tutorial code on Gradient perform the following steps:

1. Use git to clone this repo to a local folder.
2. cd tpu-mnist
3. Run `paperspace project init` to initialize a new paperspace project.
4. If you haven't already logged in to paperspace from the command line run:
   `paperspace login` and enter your credentials.
5. Run the TPU MNIST sample code as follows:

   `paperspace jobs create --machineType TPU --container gcr.io/tensorflow/tensorflow:1.6.0 --command 'export PYTHONPATH=$PYTHONPATH:/paperspace && python official/mnist/mnist_tpu.py --master=${TPU_GRPC_URL} --data_dir=gs://paperspace-mnist-tfrecords/data --model_dir=${TPU_MODEL_DIR} --use_tpu=True --iterations=500 --train_steps=1000'`

The this command uses a publicly accessible Google Cloud Storage bucket for the MNIST input data: `gs://paperspace-mnist-tfrecords/data`  The data in this bucket has already been formatted as TFRecords, as is required for tensorflow input.

The other two parameters that differ from Google's documentation are:

  `--master=${TPU_GRPC_URL}` which is used in place of the `--tpu_name` parameter.

and

  `--model_dir=${TPU_MODEL_DIR}` which is a predefined job specific storage bucket set up by Gradient for the duration of the job.

At the completion of the job any outputs written to the `--model_dir` bucket are automatically uploaded to the job's `artifacts` directory and are available via the Paperspace console for download.

