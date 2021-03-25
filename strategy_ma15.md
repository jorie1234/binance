Strategy: Back to the 15-MA

Introduction:
=============
It's a well-known fact from Technical Analysis(TA) that "the ticker always returns to the Movering Average(MA)".
Meeting with the MA might be the accurate wording, as it can happen that the MA follows the ticker.
Assuming that the ticker is not falling monotoniclly (!) that is obvious.
Using this experience, a simple strategy can be developped.


Strategy:
=========
The following is just an idea which might work. The simulation of the strategy is currently WIP!
Some bonus stuff is missing (MVP style :) ). For example, it might be useful to cancle buy orders,
if in a later iteration it is obvious the the MA strongly follows the ticker.
Depending on the percentage set for the gains it might be possible to have lots of small trades.


Parameters:
    - t_delta:  interval to check for possible buy orders (f.e. 5m)
    - dist:     distance (in percent) of the ticker from the MA (f.e. 0,5%)
    - size:     size of the MA window (f.e. 15)

Algo:
    while (TRUE)
        data[] = get_ticker_1m( timespan = now:now-range*t_delta, kind = "low")
        ma = CalcMA( data, time = now, len = size)

        if ( (data[now] / ma) < dist)

            # checks (list not complete)
            analysis_neighborhood()         # using the 1m data. f.e. find a useful price offset

            price = ticker + offset         # offset might be 0 for simplicity
            set_buy_order( price)

            gain_percent = dist * factor    # maybe dist = 1.0 or 2.0 works as well
            set_sell_order( limit = price + gain_percent)
        endif

        sleep( t_delta)
    endwhile
