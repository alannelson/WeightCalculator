






(function($) {
    $.fn.calculator = function(options) {
        var opts = $.extend($.fn.calculator.defaults, options);
        return calculate();
    };
    $.fn.calculator.defaults = {
        age: 29,
        currentWeight: 250,
        height: 72,
        activity: 0.375,
        sex: "M",
        endweight: 180,
        calories: 1500,
        losstype: "calories",
        timeStamp: new Date(),
        bmrFormula: "HB"

    };


    function CalculatorJSON(week,date,weightLost, currentWeight, bmr, activityCalories, dailyTotalExpenditure, dailyCalorieIntake, weeksTDEE, weekCalorieIntake, difference, totalLost)
    {
        this.week=week;
        this.date=date;
        this.weightLost=weightLost;
        this.currentWeight=currentWeight;
        this.bmr=bmr;
        this.activityCalories=activityCalories;
        this.dailyTotalExpenditure=dailyTotalExpenditure;
        this.dailyCalorieIntake=dailyCalorieIntake;
        this.weeksTDEE= weeksTDEE;
        this.weekCalorieIntake=weekCalorieIntake;
        this.difference=difference;
        this.totalLost=totalLost;
        
    }

    function lbsToKg(lbs)
    {
        return lbs * .45;
    }
    function kgToLbs(kg)
    {
        return kg * 2.2;
    }

    function inchesToCm(inches)
    {
        return inches * 2.54;
    }
    function cmToInches(cm)
    {
        return cm * .39;
    }

    function maleBMR(weight, height, age)
    {
        return 66 + (6.3 * weight) + (12.9 * height) - (6.8 * age);
    }

    function femaleBMR(weight, height, age)
    {
        return 655 + (4.3 * weight) + (4.7 * height) - (4.7 * age);
    }

    function maleMSJBMR(weight, height, age)
    {

        return (10.0 * lbsToKg(weight)) + (6.25 * inchesToCm(height)) - (5.0 * age) + 5;
    }

    function femaleMSJBMR(weight, height, age)
    {
        return (10.0 * lbsToKg(weight)) + (6.25 * inchesToCm(height)) - (5.0 * age) - 161;
    }
    function JSONOutput(date, lbs, newWeight, bmr, activityCalories, total, weekTotal, weekCalorieIntake, diff, week, startWeight)
    {

        var d = new Date(date);
        
        var calcJSON= new CalculatorJSON(week,
                                         d,
                                         lbs,
                                         newWeight.toFixed(2),
                                         bmr.toFixed(2),
                                         activityCalories.toFixed(2),
                                         total.toFixed(2),
                                         (weekCalorieIntake / 7).toFixed(2),
                                          weekTotal.toFixed(2),
                                          diff.toFixed(2),
                                          (startWeight - newWeight).toFixed(2)
        
        )
        return calcJSON;
    }
    function printOutput(date, lbs, newWeight, bmr, activityCalories, total, weekTotal, weekCalorieIntake, diff, week, startWeight)
    {

        var d = new Date(date);
        return " <h3>Week " + (week) + " " + d.getFullYear() + "-" + (d.getMonth() + 1) + "-" + d.getDate() + " | Weight Lost: " + lbs + " current weight: " + newWeight.toFixed(2) + "</h3>" +
                "<div>" +
                "<div> This weeks daily basal metabolic rate (BMR): " + bmr.toFixed(2) + " </div>" +
                "<div> This weeks daily calories needed for activity level: " + activityCalories.toFixed(2) + " </div>" +
                "<div> This weeks daily total daily energy expenditure (TDEE bmr + activity calories): " + total.toFixed(2) + " </div>" +
                "<div> This weeks daily calorie intake: " + (weekCalorieIntake / 7).toFixed(2) + " </div>" +
                "<div> This weeks total TDEE (bmr + activity calories x7): " + weekTotal.toFixed(2) + " </div>" +
                "<div> This weeks total calorie intake: " + weekCalorieIntake.toFixed(2) + " </div>" +
                "<div> Difference : " + diff.toFixed(2) + " </div>" +
                "<div> Pounds Lost : " + lbs + " </div>" +
                "<div> Total Pounds Lost : " + (startWeight - newWeight).toFixed(2) + " </div>" +
                "</div>";
    }

//    function calculate(age, currentWeight, height, activity, sex, endweight, calories, losstype, timeStamp, bmrFormula)
    function calculate()
    {

        var jsonOutputArray= new Array();
        var week = 0;
        var output = "";
//        var calculator = new Calculator(age, currentWeight, height, activity, sex, endweight, calories, losstype, timeStamp, bmrFormula);
        var startWeight = $.fn.calculator.defaults.currentWeight;
        while ($.fn.calculator.defaults.currentWeight > $.fn.calculator.defaults.endweight)
        {
            week++;
            var BMR;
            var weekCalorieIntake;
            var diff;
            var lbs;
            $.fn.calculator.defaults.timeStamp.setDate($.fn.calculator.defaults.timeStamp.getDate() + 7);
            if ($.fn.calculator.defaults.sex == "M")
            {
                if ($.fn.calculator.defaults.bmrFormula == "HB")
                {
                    BMR = maleBMR($.fn.calculator.defaults.currentWeight, $.fn.calculator.defaults.height, $.fn.calculator.defaults.age);
                }
                else
                {
                    BMR = maleMSJBMR($.fn.calculator.defaults.currentWeight, $.fn.calculator.defaults.height, $.fn.calculator.defaults.age);
                }
            }
            else
            {
                if ($.fn.calculator.defaults.bmrFormula == "HB")
                {
                    BMR = femaleBMR($.fn.calculator.defaults.currentWeight, $.fn.calculator.defaults.height, $.fn.calculator.defaults.age);
                }
                else
                {
                    BMR = femaleMSJBMR($.fn.calculator.defaults.currentWeight, $.fn.calculator.defaults.height, $.fn.calculator.defaults.age);
                }
            }
            var activityCalories = BMR * $.fn.calculator.defaults.activity;
            var total = BMR + activityCalories;
            var weekTotal = total * 7;
            if ($.fn.calculator.defaults.losstype == "calories")
            {
                weekCalorieIntake = $.fn.calculator.defaults.calories * 7;
                diff = weekTotal - weekCalorieIntake;
                lbs = (diff / 3500).toFixed(2);
            }
            else
            {
                lbs = $.fn.calculator.defaults.calories;
                diff = lbs * 3500;
                weekCalorieIntake = weekTotal - diff;
            }
            $.fn.calculator.defaults.currentWeight = $.fn.calculator.defaults.currentWeight - lbs;
//            output += printOutput($.fn.calculator.defaults.timeStamp, lbs, $.fn.calculator.defaults.currentWeight, BMR, activityCalories, total, weekTotal, weekCalorieIntake, diff, week, startWeight);
              jsonOutputArray.push(JSONOutput($.fn.calculator.defaults.timeStamp, lbs, $.fn.calculator.defaults.currentWeight, BMR, activityCalories, total, weekTotal, weekCalorieIntake, diff, week, startWeight));
        }
//        return output;
//        alert(JSON.stringify(jsonOutputArray));
        return JSON.stringify(jsonOutputArray);
    }


}(jQuery));