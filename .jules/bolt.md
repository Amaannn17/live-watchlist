## 2024-05-18 - Caching DOM String Computations in Polling Apps
**Learning:** In a vanilla JS app that updates via polling, blindly reconstructing the DOM innerHTML every interval for items that haven't changed leads to unneeded string concatenations and numeric conversions.
**Action:** Always hash or stringify the incoming data variables for each element being updated and compare it against the previously rendered state stored directly on the DOM element's dataset. Early return if the state hasn't changed.
