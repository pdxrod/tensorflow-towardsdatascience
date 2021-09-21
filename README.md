#### The world's first trillion-dollar company fails to support developers



The last time I experienced fail like this was twenty years ago, when I was forced to attempt to communicate with Microsoft for work.

But this is Apple. They're supposed to be different.




In March 2021, I bought a MacBook Pro with the new M1 chip, with an integrated GPU. This means you can do Artificial Intelligence and Machine Learning on it. On September 17, I finally got it working.

Various people helped me, none of them at Apple. Except for one  online chat guy. I was unable to see replies to my comments on Apple's developer site

`https://developer.apple.com/forums/thread/686926?page=1#685386022`

which might contain a solution to my problem, because I'd changed my phone number, having moved to a different country (I do that a lot), and the only way developer.apple.com would let me in would be by sending me a code on my old phone. Anyway, the guy on the chat line enabled me to send them a message, and they say they might be able to let me in some time today.

Meantime, I figured out how to do what I wanted, with no help from Apple.

See

https://stackoverflow.com/questions/56604348/how-to-install-tensorflow-2-0-on-mac-or-linux

The instructions at `https://github.com/apple/tensorflow_macos` tell you to do this

`/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/apple/tensorflow_macos/master/scripts/download__install.sh)"`

but then this script tells you to run a file which doesn't exist.

Four other developers have the same problem. The last comment is June 3rd. I eventually sent emails to all the email addresses of the contributors I could find listed at https://github.com/apple/tensorflow_macos, but none of them replied. The repository is now read-only, and archived, allowing no more comments. I doubt if Github would allow just anyone to register `github.com/apple`, so I suspect it's only for Apple employees.

The world's first trillion-dollar company is unable to support one of its claims about its new computer - that it can be used to do machine learning in Python using Tensorflow. Contrast this with my experience of the open-source programming language Elixir. Every question I have asked at https://elixirforum.com/ got answered within 24 hours by the creator of the language, Jose Valim.

After five months, I did eventually get Tensorflow working as advertised on my Mac M1.

Thanks https://towardsdatascience.com/installing-tensorflow-on-the-m1-mac-410bb36b776

I needed to download from `https://github.com/conda-forge/miniforge/releases` and run `Miniforge3-MacOSX-arm64.sh` several times to get it to install a lot of software in `/Users/rod/miniforge3`

See also
https://medium.com/gft-engineering/macbook-m1-tensorflow-on-jupyter-notebooks-6171e1f48060
who made the following useful comment:

"After publishing the article, someone reached me with this error when installing TensorFlow:
ERROR: tensorflow_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl is not a supported wheel on this platform.
This happened because Anaconda was installed. As I describe above, Anaconda is not ARM compatible, so the most direct way to solve this is to uninstall Anaconda and install Miniforge instead."

`$ brew uninstall anaconda`

This made all my other python programs not work, so I had to redirect a series of soft links to point to `/Users/rod/minforge3/bin`.

However, using Tensorflow still involves using a version of Anaconda - this one:

`/Users/rod/miniforge3/bin/conda`

And you do `conda activate apple_tensorflow` before running a Tensorflow program.

The program won't run like this:

`/Users/rod/miniforge3/bin/python my_tensorflow_program.py`

Nor will it from from the command line if you put

`#!/Users/rod/miniforge3/bin/python`

at the top.

But if you put

`#!python`

at the top, it figures it out.

```
$conda activate apple_tensorflow

$ which python

/Users/rod/miniforge3/envs/apple_tensorflow/bin/python
```

This is Python 3.9.6

I also got help from https://medium.com/codex/installing-tensorflow-on-m1-macs-958767a7a4b3

At this point, I have to admit part of the delay was my bad. I didn't read the instructions clearly. You have to do the following, in this order, in folder miniforge3/ -

    conda env create environment.yml
    conda activate apple_tensorflow
    pip install --upgrade --force --no-dependencies https://github.com/apple/tensorflow_macos/releases/download/v0.1alpha3/tensorflow_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl https://github.com/apple/tensorflow_macos/releases/download/v0.1alpha3/tensorflow_addons_macos-0.1a3-cp38-cp38-macosx_11_0_arm64.whl```

    conda install notebook -y
    conda install matplotlib -y
    conda install pandas -y
    conda install scikit-learn -y
    jupyter notebook


Soon, I'll be writing code like this

https://colab.research.google.com/github/ageron/handson-ml/blob/master/01_the_machine_learning_landscape.ipynb

and be head-hunted by DeepMind

https://github.com/deepmind/alphafold
