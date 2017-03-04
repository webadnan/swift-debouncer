# Debouncer Class
    // file: Debouncer.swift
    import Foundation

    class Debouncer: NSObject {
        var callback: (() -> ())
        var delay: Double
        weak var timer: Timer?

        init(delay: Double, callback: @escaping (() -> ())) {
            self.delay = delay
            self.callback = callback
        }

        func call() {
            timer?.invalidate()
            let nextTimer = Timer.scheduledTimer(timeInterval: delay, target: self, selector: #selector(Debouncer.fireNow), userInfo: nil, repeats: false)
            timer = nextTimer
        }

        func fireNow() {
            self.callback()
        }
    }


# USAGES
    let debouncedFunction = Debouncer(delay: 0.40) {
        print("delayed printing")
    }
    
    debouncedFunction.call()
    debouncedFunction.call()
    debouncedFunction.call()
    debouncedFunction.call()
    debouncedFunction.call()

It works like JavaScript's debounce function, for example http://modernjavascript.blogspot.com/2013/08/building-better-debounce.html

# About Debounce
The debounce function is an extremely useful tool that can help throttle requests. It is different to throttle though as throttle will allow only one request per time period, debounce will not fire immediately and wait the specified time period before firing the request. If there is another request made before the end of the time period then we restart the count. This can be extremely useful for calling functions that often get called and are only needed to run once after all the changes have been made.
