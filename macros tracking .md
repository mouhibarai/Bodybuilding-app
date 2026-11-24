# Bodybuilding-app
Open-source fitness coaching intake, macronutrient calculator, and hypertrophy tracking logic.
// Open-Source Bodybuilding & Coaching Macronutrient Calculator
function calculateMacros({ weightKg, heightCm, age, activityMultiplier, goal }) {
  const bmr = 10 * weightKg + 6.25 * heightCm - 5 * age + 5;
  const tdee = Math.round(bmr * activityMultiplier);

  const calorieTargets = {
    cut: tdee - 450,
    recomp: tdee,
    bulk: tdee + 300
  };

  const targetCalories = calorieTargets[goal] || tdee;
  const proteinGrams = Math.round(weightKg * 2.2);
  const fatGrams = Math.round(weightKg * 0.8);
  const carbGrams = Math.max(0, Math.round((targetCalories - (proteinGrams * 4 + fatGrams * 9)) / 4));

  return { targetCalories, proteinGrams, fatGrams, carbGrams };
}

module.exports = { calculateMacros };
