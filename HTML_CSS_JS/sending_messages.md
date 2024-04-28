<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# Messages

## Table of Contents
<!-- TOC -->

- [Messages](#messages)
	- [Table of Contents](#table-of-contents)
	- [EmailJS](#emailjs)
		- [EmailJS in React](#emailjs-in-react)

<!-- /TOC -->

## [EmailJS](#table-of-contents)
1. Sign Up or Login
1. Email Services -> Add New Service
1. Connect Account-> Login into your email.
1. Create Service
1. Email Template -> Create New Template
1. In your form in JS make sure to make the name the same as inside the {{}}s

| Keys        | Location                                           |
|-------------|----------------------------------------------------|
| Service Id  | Email Services -> Click your service               |
| Template Id | Email Templates -> Click your template -> Settings |
| Public Key  | Account                                            |

### [EmailJS in React](#table-of-contents)
`npm install @emailjs/browser`

```javascript
import { useState, useRef } from 'react'
import emailjs from '@emailjs/browser'

export default function Email(){
  const form = useRef()
  const [name, setName] = useState("")
  const [email, setEmail] = useState("")
  const [message, setMessage] = useState("")

  async function sendEmail(event){
      event.preventDefault()
      const serviceId = "YOUR_SERVICE_ID"
      const templateId = "YOUR_TEMPLATE_ID"
      const publicKey = "YOUR_PUBLIC_KEY"
      try{
        const result = await emailjs.sendForm(serviceId, templateId, form.current, publicKey)
        console.log(result.text)
        setName("")
        setEmail("")
        setMessage("")
      }catch(error){
        console.log(error.text);
      }
  }

  return (
    <form ref={form} onSubmit={sendEmail}>
      <input type="text" name="user_name" value={name} onChange={(event) => {setName(event.value)}}/>
      <input type="email" name="user_email" value={email} onChange={(event) => {setEmail(event.value)}}/>
      <textarea name="message" value={message} onChange={(event) => {setMessage(event.value)}}/>
      <button type="submit" value="Send" />
    </form>
  )
}
```