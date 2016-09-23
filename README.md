# audio_waveform-ruby

[![Gem Version](https://badge.fury.io/rb/audio_waveform-ruby.svg)](http://rubygems.org/gems/audio_waveform-ruby) [![Build Status](https://travis-ci.org/bbc/audio_waveform-ruby.svg?branch=master)](https://travis-ci.org/bbc/audio_waveform-ruby)

The audio_waveform-ruby gem provides a Ruby API for access to audio waveform data
files generated by the [audiowaveform](https://github.com/bbc/audiowaveform) program.

Refer to the [audiowaveform](https://github.com/bbc/audiowaveform) documentation for more information and [this page](https://github.com/bbc/audiowaveform/blob/master/doc/DataFormat.md) for file format details.

## Installation

To install:

    $ gem install audio_waveform-ruby

or, if using bundler, add this line to your application's Gemfile:

    gem 'audio_waveform-ruby', :require => 'audio_waveform'

or, to use the latest code from the GitHub repository:

    gem 'audio_waveform-ruby', :require => 'audio_waveform',
        :git => 'https://github.com/bbc/audio_waveform-ruby.git'

and run

    $ bundle install

## Usage

To use this Gem in your program, add:

    require 'audio_waveform'

Then, to load and use data from an existing waveform data file:

    waveform = AudioWaveform::WaveformDataFile.new(filename: "test.dat")

    puts waveform.sample_rate       # Returns audio sample rate, in Hz
    puts waveform.bits              # Returns resolution of waveform data points
    puts waveform.samples_per_pixel # Returns waveform zoom level, in samples per pixel
    puts waveform.length            # Returns number of waveform data points

    (0...waveform.length).each do |i|
      puts waveform.min(i)   # Returns waveform minimum at index i
      puts waveform.max(i)   # Returns waveform maximum at index i
    end

To generate a binary representation of a waveform data file:

    waveform = AudioWaveform::WaveformDataFile.new(filename: "test.dat")
    data = waveform.to_binary

To save waveform data as a file in binary format:

    waveform = AudioWaveform::WaveformDataFile.new(filename: "test.dat")
    waveform.save_as_binary("output.dat")

To generate a JSON representation of a waveform data file:

    waveform = AudioWaveform::WaveformDataFile.new(filename: "test.dat")
    waveform.to_json

To save waveform data as a file in JSON format:

    waveform = AudioWaveform::WaveformDataFile.new(filename: "test.dat")
    waveform.save_as_json("output.json")

To create a new waveform data file:

    waveform = AudioWaveform::WaveformDataFile.new(
        sample_rate: 44100,
        samples_per_pixel: 512,
        bits: 8
    )

    waveform.append(-10, 10)
            .append(-11, 11)
            .append(-3, 3)
    # etc

## License

See COPYING for details.

## Contributing

If you have a feature request or want to report a bug, we'd be happy to hear from you. Please either raise an [issue](https://github.com/bbcrd/audio_waveform-ruby/issues), or fork the project and send us a pull request.

## Authors

This software was written by [Chris Needham](https://github.com/chrisn), chris.needham at bbc.co.uk.

## Copyright

Copyright 2013-2016 British Broadcasting Corporation
