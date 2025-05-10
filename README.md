def plan_itinerary(self, days: int, attractions: List[str]) -> Dict:
        """规划行程"""
        if days <= 0:
            return {"error": "天数必须大于0"}
        
        # 简单分配景点到每天
        itinerary = {}
        attractions_per_day = []
        
        if days >= len(attractions):
            # 如果天数足够，每天去1-2个景点
            for i in range(len(attractions)):
                day = i % days + 1
                if day not in itinerary:
                    itinerary[day] = []
                itinerary[day].append(attractions[i])
        else:
            # 如果天数不足，平均分配
            import math
            per_day = math.ceil(len(attractions) / days)
            for i in range(days):
                start = i * per_day
                end = start + per_day
                itinerary[i+1] = attractions[start:end]
        
        return itinerary
