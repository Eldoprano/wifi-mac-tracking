# Modified source from: "Non-cooperative 802.11 MAC layer fingerprinting and tracking of mobile devices"
This repository contains a modified source code used in the paper entitled "Non-cooperative 802.11 MAC layer fingerprinting and tracking of mobile devices". Please cite the paper and / or datasets if you use them in your research.

## Downloading the datasets
The two datasets used can be found here:
- [Local Dataset](https://crawdad.org/nile/probe-requests/2021-06-28/)
- [Universal Dataset](https://data.mendeley.com/datasets/j64btzdsdy/1)

## Running experiments
To run this script, you will need to install Python 2.7, and the necessary libraries.
After downloading the datasets, you can run the experiments using the ```elt_byte_uniqueness.py``` script:

    usage: elt_byte_uniqueness.py [-h] [--host HOST] [--debug] [--big-endian]
                                  [--train-samples NUM_TRAIN_SAMPLES]
                                  [--test-samples NUM_TEST_SAMPLES]
                                  [--threshold THRESHOLD]
                                  {mongodb,file,pcap} {mac_info,mac_research}

    Advanced MAC layer fingerprinter for Probe Request frames

    positional arguments:
      {mongodb,file,pcap}
      {mac_info,mac_research}
                            The path to / name of the dataset containing Probe
                            Requests

    optional arguments:
      -h, --help            show this help message and exit
      --host HOST           MongoDB host (default: localhost)
      --debug, -d           Debug mode (default: False)
      --big-endian          Big Endian Radiotap header (default: False)
      --train-samples NUM_TRAIN_SAMPLES
                            Number of training samples (default: 30000)
      --test-samples NUM_TEST_SAMPLES
                            Number of test samples (default: 50)
      --threshold THRESHOLD
                            Stability threshold (default: 0.3)

## Examples

The command used for the experiments of the paper is:

    $ ./elt_byte_uniqueness.py pcap <path_to_PCAP_file>

## Explanation of metrics
After running ```elt_byte_uniqueness.py```, several metrics are displayed to the user, which have the following meaning:

* Strict hash stability           : Average ratio of devices with a stable hash to all devices
* Real hash stability             : Average ratio of most prominent hash to to all hashes for each device
* Real hash stability (non-random): Average ratio of most prominent hash to to all hashes for each device with non-random MAC
* Hash uniqueness                 : Ratio of unique IE hashes to all IE hashes for random MACs
* Hash uniqueness (non-random)    : Ratio of unique IE hashes to all IE hashes for non-random MACs
* Fingerprint uniqueness          : Ratio of unique fingerprints to all fingerprints
* Deanonymized MACs               : Number of random MACs successfully mapped to non-random MACs
* Total MACs                      : Number of unique MAC addresses in test set

Here, the term "hash" refers to the hash of the bitmask applied to the Information Elements of the Probe Request, and the term "fingerprint" refers to the associated fingerprint (which can include the non-random MAC address as well if available).