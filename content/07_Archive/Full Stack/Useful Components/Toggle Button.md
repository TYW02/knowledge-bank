

# Toggle State
```jsx
// Toggle button
    const [isOn, setIsOn] = useState(false);
    
    const handleToggle = () => {
        setIsOn(prev => !prev)
        // If `prev` is `true` `!prev` will be `false`
        // If `prev` is `false` `!prev` will be `true`
    }
```
- This pattern is typically used to toggle boolean state variable
	- We are using this to toggle between "ON" & "OFF"


# Toggle Button
```jsx
<div className="reminder-toggle">
  <div className={`toggle-switch ${isOn ? 'on' : ''}`} onClick={handleToggle}>
    <div className="toggle-knob"></div>
  </div>
</div>
```


# Toggle CSS
```css
.reminder-toggle {
    display: flex;
    align-items: center;
    justify-content: center;
}

.toggle-switch {
    width: 50px;
    height: 28px;
    background-color: #555;
    border-radius: 999px;
    position: relative;
    /*relative position to allow knob to make reference to switch position */
    cursor: pointer;
    transition: background-color 0.3s ease;
}
  
.toggle-switch.on {
    background-color: #8b5cf6;
}
  
.toggle-knob {
    width: 22px;
    height: 22px;
    background-color: #e5e7eb;
    border-radius: 50%;
    position: absolute;
    /*now knob will take its position (top 3px, left 3px) relative to switch */
    top: 3px;
    left: 3px;
    transition: transform 0.3s ease;
}

.toggle-switch.on .toggle-knob {
    transform: translate(22px)
    /*translate "moves" the element from its position by the given amount */
}
```


# What each CSS property do

- Red Border highlights which part it is and has nothing to do with the design

# .reminder-toggle
![[Pasted image 20250719230435.png]]

# .toggle-switch
![[Pasted image 20250719230310.png]]

# .toggle-knob
![[Pasted image 20250719230517.png]]

































