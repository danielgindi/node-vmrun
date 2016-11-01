# vmrun

[![npm Version](https://badge.fury.io/js/vmrun.png)](https://npmjs.org/package/vmrun)

A wrapper for VMWare CLI (vmrun) with Promises,

## Includes:

* Full `stdout`/`stderr` output
* Possibility to run an "unimplemented" vmrun feature using the `.vmrun(...)` call
* Interfaces for many of the common features like starting/stopping a VM, taking snapshots, running and killing processes, moving/copying files between host and guest etc.
* Crossplatform

## Installation:

```
npm install --save vmrun
```

## Usage example:

```javascript

var VMRun = require('vmrun');

VMRun.setOptions({
    hostType: 'ws' // Workstation
    , guestUsername: 'user'
    , guestPassword: '1234'
});

VMRun
  .start('/home/user/vmware/machine/machine.vmx')
  .then(function () {
    return VMRun.poweroff('/home/user/vmware/otherMachine/otherMachine.vmx')
  })
  .catch(function (err) {
    console.log(err);
  })

```

Another way of setting options for controlling the vms, is using `VMRun.withOptions(options)` to get a new VMRun instance with the new options,
or using `VMRun.withModifiedOptions(options)` to get a new VMRun instance with the new options inheriting from the current options.

```
var VMRun = require('vmrun')
    .setOptions({
        hostType: 'ws'
    });

VMRun
    .withModifiedOptions({ guestUsername: 'user1', guestPassword: '123' })
    .deleteFileInGuest('/home/user/vmware/machine/machine.vmx', 'C:\\Windows\\Temp\\temp.file')
    .then(function (std) {

    });

VMRun
    .withModifiedOptions({ guestUsername: 'user2', guestPassword: '123' })
    .deleteFileInGuest('/home/user/vmware/machine/machine.vmx', 'C:\\Windows\\Temp\\temp.file')
    .then(function (std) {

    });

```

Options for configuring VMRun are:
* {String?} hostName
* {Number?} hostPort
* {VMWareHostType?} hostType
* {String?} hostUsername
* {String?} hostPassword
* {String?} guestUsername
* {String?} guestPassword
* {String?} vmPassword

Host types are:
* 'ws' = VMWare Workstation
* 'server1' = VMWare Server 1.0
* 'server' = VMWare Server 2.0
* 'ws-shared' = VMWare Workstation (Shared Mode)
* 'esx' = VMWare ESX
* 'vc' = VMWare vCenter Server

All options are in the JSDocs!

## Contributing

If you have anything to contribute, or functionality that you lack - you are more than welcome to participate in this!
If anyone wishes to contribute unit tests - that also would be great :-)

## Me
* Hi! I am Daniel Cohen Gindi. Or in short- Daniel.
* danielgindi@gmail.com is my email address.
* That's all you need to know.

## Help

If you want to buy me a beer, you are very welcome to
[![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donate_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=G6CELS3E997ZE)
 Thanks :-)

## License

All the code here is under MIT license. Which means you could do virtually anything with the code.
I will appreciate it very much if you keep an attribution where appropriate.

    The MIT License (MIT)

    Copyright (c) 2013 Daniel Cohen Gindi (danielgindi@gmail.com)

    Permission is hereby granted, free of charge, to any person obtaining a copy
    of this software and associated documentation files (the "Software"), to deal
    in the Software without restriction, including without limitation the rights
    to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
    copies of the Software, and to permit persons to whom the Software is
    furnished to do so, subject to the following conditions:

    The above copyright notice and this permission notice shall be included in all
    copies or substantial portions of the Software.
