# A faulted component latches its fault and keeps the span

When a commanded movement (barriers or span) is not confirmed in time, the component that commanded it enters a fault and raises the alarm. It never releases the span, and it ignores everything until restart: there is no reset. Keeping the span freezes the other side without any broadcast message. If the barriers stick, boats wait forever. If the span sticks, nobody is granted it. Safety comes before service: every bounded-response property holds "unless a fault occurs first". This follows the airlock's D7.
