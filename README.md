# Virtual Keyboard Unity3D

# Introduction

**HGS Tone** is a Synthsizer and Midi Player wrapper of [MeltySynth](https://github.com/sinshu/meltysynth) for Unity. This package turns possible play musical notes from all part of your UnityProject. Click in this image above to see youtube vídeo.

Requires Unity 2021 or bigger.

![demo](Demos/virtual%20keyboard.gif)

## Playing Musical Notes

Play note and release after default time

```cs
using HGS.Tone

public class Player: MonoBehaviour
{
  [SerializeField] ToneSynth synth;

  void Start()
  {
   synth.TriggerAttackAndRelease(ToneNote.Parse("C3"));
  }
}
```

Play note and release after 3 seconds

```cs
using HGS.Tone

public class Player: MonoBehaviour
{
  [SerializeField] ToneSynth synth;

  void Start()
  {
   synth.TriggerAttackAndRelease(ToneNote.Parse("C3"), duration:3);
  }
}
```

Play note with custom release

```cs
using HGS.Tone

public class Player: MonoBehaviour
{
  [SerializeField] ToneSynth synth;

  void Update()
  {
    if(Input.GetKeyDown(KeyCode.C)) synth.TriggerAttack(ToneNote.Parse("C3"));
    if(Input.GetKeyUp(KeyCode.C)) synth.TriggerRelease(ToneNote.Parse("C3"));
  }
}
```

## Changing instrument

Use `MidiInstrumentCode` to access Midi instrument list available.

```cs
using HGS.Tone

public class Player: MonoBehaviour
{
  [SerializeField] ToneSynth synth;

  void Start()
  {
    synth.SetInstrument(MidiInstrumentCode.Organ_Accordion);
  }
}
```

## Playing Midi files

From `Resources` folder
| Attention: for read midi files from resources, you need change file extension from `.midi` to `.bytes`.

```cs
using HGS.Tone

public class Player: MonoBehaviour
{
  [SerializeField] ToneSequencer sequencer;

  void Start()
  {
    var path = "you/path/to/midifile";
    sequencer.Play(path);
  }
}
```

From others sources

```cs
using HGS.Tone

public class Player: MonoBehaviour
{
  [SerializeField] ToneSequencer sequencer;

  void Start()
  {
    var bytes = new byte[]{}; // you file bytes
    var stream = new MemoryStream(bytes);
    sequencer.Play(stream);
  }
}
```

## MidiMessage Events

`ToneSequencer` and `ToneSynth` contains `onMidiMessage`:

```cs
using HGS.Tone

public class CallbackLogger: MonoBehaviour
{
  [SerializeField] ToneSequencer sequencer;

  void Start()
  {
    sequencer.onMidiMessage += HandleOnMidiMessage;
  }

  void HandleOnMidiMessage(int channel, int command, int data1, int data2)
  {
    Debug.Log($"MidiMessageCallback: {channel}, {command}, {data1}, {data2}");
  }
}
```

## Installation

OpenUPM:

`openupm add com.hgs.tone`

Package Manager:

`https://github.com/homy-game-studio/hgs-unity-tone.git#upm`

Or specify version:

`https://github.com/homy-game-studio/hgs-unity-tone.git#1.0.0`