# AdditionPracticeGame
using UnityEngine;
using UnityEngine.UI;

public class GameManager : MonoBehaviour
{
    public Text problemText;
    public InputField answerInput;
    public Text timerText;
    public Text scoreText;
    
    private int number1;
    private int number2;
    private int score;
    private float timer = 60f;
    private bool isGameOver = false;

    void Start()
    {
        GenerateProblem();
        UpdateScore();
    }

    void Update()
    {
        if (!isGameOver)
        {
            timer -= Time.deltaTime;
            timerText.text = "Time: " + Mathf.Round(timer).ToString();
            
            if (timer <= 0)
            {
                EndGame();
            }
        }
    }

    public void CheckAnswer()
    {
        int playerAnswer;
        if (int.TryParse(answerInput.text, out playerAnswer))
        {
            if (playerAnswer == number1 + number2)
            {
                score++;
                UpdateScore();
            }
            answerInput.text = "";
            GenerateProblem();
        }
    }

    void GenerateProblem()
    {
        number1 = Random.Range(0, 13);
        number2 = Random.Range(0, 13);
        problemText.text = number1.ToString() + " + " + number2.ToString() + " = ?";
    }

    void UpdateScore()
    {
        scoreText.text = "Score: " + score.ToString();
    }

    void EndGame()
    {
        isGameOver = true;
        problemText.text = "Game Over!";
    }
}
