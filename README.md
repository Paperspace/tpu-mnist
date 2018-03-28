# Gradient changes to Google's TPU MNIST tutorial

These source files are taken from the Google [TPU MNIST tutorial](https://cloud.google.com/tpu/docs/tutorials/mnist).  The actual files are included on the Google vm image referenced in the tutorial (`image-project=ml-images`, `image-family=tf-1-6`). The original source files are unchanged, but the way the sample is run is slightly different in Paperspace Gradient.

You can learn more about Paperspace Gradient [here](https://www.paperspace.com/gradient).

Note: the original README file for these sources is [README_ORIG.md](README_ORIG.md)

To run the MNIST tutorial code on Gradient perform the following steps:

1. Use git to clone this repo to a local folder.
2. cd tpu-mnist
3. Run `paperspace project init` to initialize a new paperspace project.
4. If you haven't already logged in to paperspace from the command line run:
   `paperspace login` and enter your credentials.
5. Run the TPU MNIST sample code as follows:

   `paperspace jobs create --machineType TPU --container gcr.io/tensorflow/tensorflow:1.6.0 --command 'python official/mnist/mnist_tpu.py --master=${TPU_GRPC_URL} --data_dir=gs://paperspace-mnist-tfrecords/data --model_dir=${TPU_MODEL_DIR} --use_tpu=True --iterations=500 --train_steps=1000'`

The this command uses a publicly accessible Google Cloud Storage bucket for the MNIST input data_dir parameter:

  `--data_dir=gs://paperspace-mnist-tfrecords/data`  The data in this bucket has already been formatted as TFRecord objects.

The other parameter changes are:

  `--master=${TPU_GRPC_URL}` which is used in place of the `--tpu_name` parameter.

and

  `--model_dir=${TPU_MODEL_DIR}` which is a predefined job specific storage bucket set up by Gradient for the duration of the job.

At the completion of the job any outputs written to the `--model_dir` bucket are automatically uploaded to the job's `artifacts` directory and are available via the Paperspace console for download.

