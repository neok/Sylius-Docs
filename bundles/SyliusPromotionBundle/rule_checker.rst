How rules are checked ?
=======================

Everything related to this subject is located in ``Sylius\Bundle\PromotionsBundle\Checker``.

Rule checkers
-------------

New rules can be created by implementing ``RuleCheckerInterface``. This interface provides the method ``isEligible`` which aims to determine if the promotion subject respects the current rule or not.

I told you before that ``SyliusPromotionsBundle`` ships with 2 types of rules : item count rule and item total rule.

Item count rule is defined via the service ``sylius.promotion_rule_checker.item_count`` which uses the class ``ItemCountRuleChecker``. The method ``isEligible`` checks here if the promotion subject has the minimum number of items (method ``getPromotionSubjectItemCount()`` of ``PromotionSubjectInterface``) required by the rule.

Item total rule is defined via the service ``sylius.promotion_rule_checker.item_total`` which uses the class ``ItemTotalRuleChecker``. The method ``isEligible`` checks here if the promotion subject has the minimum amount (method ``getPromotionSubjectItemTotal()`` of ``PromotionSubjectInterface``) required by the rule.


The promotion eligibility checker service
-----------------------------------------

To be eligible to a promotion, a subject must :

1. respect all the rules related to the promotion
2. respect promotion dates if promotion is limited by time
3. respect promotions usages count if promotion has a limited number of usages
4. if a coupon is provided with this order, it must be valid and belong to this promotion

The service ``sylius.promotion_eligibility_checker`` checks all these constraints for you with the method ``isEligible()``  which returns ``true`` or ``false``. This service uses the class ``PromotionEligibilityChecker``.

