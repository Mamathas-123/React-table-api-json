# React-table-api-json

import React, {useEffect, useState} from 'react'
import ReactDOM from 'react-dom'
import axios from 'axios'

function App() {
  const [data, setData] = useState([])
  const [loading, setLoading] = useState(true)

  useEffect(() => {
    axios
      //.get('https://jsonplaceholder.typicode.com/users')   //this is API json data
      .get('https://opentdb.com/api.php?amount=50')
      .then(response => {
        setData(response.data.results)
        console.log('data', response.data.results)
        setLoading(false)
      })
      .catch(error => {
        console.log(error)
      })
  }, [])
  return (
    <div>
      <h2>Table data from API/JSON</h2>
      {loading ? (
        <div>Loading...</div>
      ) : (
        <table border={1}>
          <tr>
            <th>Id</th>
            <th>Type</th>
            <th>Question</th>
            <th>Answer</th>
          </tr>
          {data.map((item, index) => {
            return (
              <tr key={index}>
                <td>{index + 1}</td>
                <td>{item.type}</td>
                <td>{item.question}</td>
                <td>{item.correct_answer}</td>
              </tr>
            )
          })}
        </table>
      )}
    </div>
  )
}

ReactDOM.render(<App />, document.getElementById('root'))
