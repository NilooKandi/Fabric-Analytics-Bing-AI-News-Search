```DAX

Positive Sentiment % = 
IF (
    COUNTROWS (
        FILTER (
            'tbl_sentiment_analysis', 
            'tbl_sentiment_analysis'[sentiment] = "positive"
        )
    ) > 0,
    DIVIDE (
        COUNTROWS (
            FILTER (
                'tbl_sentiment_analysis', 
                'tbl_sentiment_analysis'[sentiment] = "positive"
            )
        ),
        COUNTROWS ('tbl_sentiment_analysis')
    ),
    0
)



Negative Sentiment % = 
IF (
    COUNTROWS (
        FILTER (
            'tbl_sentiment_analysis', 
            'tbl_sentiment_analysis'[sentiment] = "negative"
        )
    ) > 0,
    DIVIDE (
        COUNTROWS (
            FILTER (
                'tbl_sentiment_analysis', 
                'tbl_sentiment_analysis'[sentiment] = "negative"
            )
        ),
        COUNTROWS ('tbl_sentiment_analysis')
    ),
    0
)




Neutral Sentiment % = 
IF (
    COUNTROWS (
        FILTER (
            'tbl_sentiment_analysis', 
            'tbl_sentiment_analysis'[sentiment] = "neutral"
        )
    ) > 0,
    DIVIDE (
        COUNTROWS (
            FILTER (
                'tbl_sentiment_analysis', 
                'tbl_sentiment_analysis'[sentiment] = "neutral"
            )
        ),
        COUNTROWS ('tbl_sentiment_analysis')
    ),
    0
)
